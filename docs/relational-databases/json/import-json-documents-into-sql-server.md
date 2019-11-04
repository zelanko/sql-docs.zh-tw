---
title: 將 JSON 文件匯入 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6a69047ca62f60cf071ac44e87bd741feea9b88
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049885"
---
# <a name="import-json-documents-into-sql-server"></a>將 JSON 文件匯入 SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文描述如何將 JSON 檔案匯入 SQL Server 中。 目前，檔案中儲存有許多 JSON 文件。 應用程式記錄資訊儲存在 JSON 檔案中、感應器所產生的資訊儲存在 JSON 檔案中，以此類推。 請務必要能夠讀取檔案中所儲存的 JSON 資料、將資料載入至 SQL Server，以及對它進行分析。

## <a name="import-a-json-document-into-a-single-column"></a>將 JSON 文件匯入至單一資料行

**OPENROWSET(BULK)** 是可從本機磁碟機或網路上之任何檔案讀取資料的資料表值函式，如果 SQL Server 具有該位置的讀取權限的話。 它會傳回具有包含檔案內容之單一資料行的資料表。 您有各種選項可以與 OPENROWSET(BULK) 函式搭配使用，例如分隔符號。 但最簡單的情況是您可以只將檔案的整個內容載入為文字值。 (這個單一大數值稱為單一字元大型物件或 SINGLE_CLOB)。 

以下是 **OPENROWSET(BULK)** 函式範例，可讀取 JSON 檔案內容，並將它以單一值形式傳回給使用者：

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j;
```

OPENJSON(BULK) 會讀取檔案的內容，並將它傳回至 `BulkColumn`。

您也可以將檔案內容載入至區域變數或資料表，如下列範例所示：

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

在載入 JSON 檔案的內容之後，您可以將 JSON 文字儲存在資料表中。


## <a name="import-json-documents-from-azure-file-storage"></a>從 Azure 檔案儲存體匯入 JSON 文件

您可以使用上述的 OPENROWSET(BULK)，從 SQL Server 可存取的檔案位置讀取 JSON 檔案。 例如，Azure 檔案儲存體支援 SMB 通訊協定。 因此，您可以使用下列程序將本機虛擬磁碟機對應至 Azure 檔案儲存體共用︰

1.  使用 Azure 入口網站或 Azure PowerShell，來建立檔案儲存體帳戶 (例如，`mystorage`)、檔案共用 (例如，`sharejson`) 以及 Azure 檔案儲存體中的資料夾。
2.  將部分 JSON 檔案上傳至檔案儲存體共用。
3.  在允許連接埠 445 的電腦上，於 Windows 防火牆中建立輸出防火牆規則。 請注意，您的網際網路服務提供者可能會封鎖此連接埠。 如果您在下一個步驟中收到 DNS 錯誤 (錯誤 53)，則尚未開啟連接埠 445，或 ISP 予以封鎖。
4. 將 Azure 檔案儲存體共用掛接為本機磁碟機 (例如 `T:`)。

    以下是命令語法：

    ```dos
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    以下是將本機磁碟機代號 `T:` 指派給 Azure 檔案儲存體共用的範例：

    ```dos
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    您可以在 Azure 入口網站之 [設定] 的 [金鑰] 區段中找到儲存體帳戶金鑰以及主要或次要儲存體帳戶存取金鑰。

5.  現在，您可以使用對應磁碟機，從 Azure 檔案儲存體存取 JSON 檔案，如下列範例所示：

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

如需 Azure 檔案儲存體的詳細資訊，請參閱[檔案儲存體](https://azure.microsoft.com/services/storage/files/)。

## <a name="import-json-documents-from-azure-blob-storage"></a>從 Azure Blob 儲存體匯入 JSON 文件

您可以使用 T-SQL BULK INSERT 命令或 OPENROWSET 函數，將檔案直接從 Azure Blob 儲存體載入至 Azure SQL Database。

請先建立外部資料來源，如下列範例所示。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

接下來，請使用 DATA_SOURCE 選項執行 BULK INSERT 命令。

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

## <a name="parse-json-documents-into-rows-and-columns"></a>將 JSON 文件剖析成資料列和資料行

您可能想要剖析 JSON 檔案，並傳回檔案中的書籍以及其資料列和資料行中的屬性，而不是讀取整個 JSON 檔案作為單一值。 下列範例使用的 JSON 檔案來自[此網站](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json)，其中包含書籍清單。

### <a name="example-1"></a>範例 1

最簡單的範例是您只要從檔案載入整個清單即可。 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

上述 OPENROWSET 會從檔案讀取單一文字值。 OPENROWSET 會傳回值作為 BulkColumn，並將 BulkColumn 傳遞至 OPENJSON 函式。 OPENJSON 會逐一查看 BulkColumn 陣列中的 JSON 物件陣列，並在每個資料列中傳回一本書。 每個資料列都會格式化為 JSON，如下所示。

```json
{"id":"978-0641723445", "cat":["book","hardcover"], "name":"The Lightning Thief", ... }
{"id":"978-1423103349", "cat":["book","paperback"], "name":"The Sea of Monsters", ... }
{"id":"978-1857995879", "cat":["book","paperback"], "name":"Sophie's World : The Greek", ... } 
{"id":"978-1933988177", "cat":["book","paperback"], "name":"Lucene in Action, Second", ... }
```

### <a name="example-2"></a>範例 2

OPENJSON 函式可以剖析 JSON 內容，並將它轉換成資料表或結果集。 下列範例會載入內容、剖析載入的 JSON，並將五個欄位傳回為資料行︰

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

在此範例中，OPENROWSET(BULK) 會讀取檔案內容，並將該內容傳遞給包含輸出之已定義結構描述的 OPENJSON 函式。 OPENJSON 使用資料行名稱來符合 JSON 物件中的屬性。 例如，`price` 屬性會以 `price` 資料行形式傳回並轉換為浮點資料類型。 以下是結果：

|Id|[屬性]|price|pages_i|作者|
|---|---|---|---|---|
|978-0641723445|The Lightning Thief|12.5|384|Rick Riordan| 
|978-1423103349|The Sea of Monsters|6.49|304|Rick Riordan| 
|978-1857995879|Sophie's World :The Greek Philosophers|3.07|64|Jostein Gaarder| 
|978-1933988177|Lucene in Action, Second Edition|30.5|475|Michael McCandless|
||||||

現在，您可以將此資料表傳回給使用者，或將資料載入至另一張資料表。

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>深入了解 SQL Server 和 Azure SQL Database 中的 JSON  
  
### <a name="microsoft-videos"></a>Microsoft 影片

如需 SQL Server 和 Azure SQL Database 中內建 JSON 支援的觀看式簡介，請參閱下列影片：

-   [SQL Server 2016 和 JSON 支援](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [使用 SQL Server 2016 和 Azure SQL Database 中的 JSON](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL 與關聯式領域之間的橋樑 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>另請參閱

[使用 OPENJSON 將 JSON 資料轉換成資料列和資料行](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)

