---
title: 使用 BULK INSERT 或 OPENROWSET(BULK...) 將資料匯入 SQL Server
description: 了解如何使用 Transact-SQL 陳述式將資料從檔案大量匯入 SQL Server 或 Azure SQL Database 資料表，包括安全性考量。
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
author: markingmyname
ms.author: maghan
manager: jroth
ms.date: 09/25/2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: fe9d407b446177004715ae5d3403e856028985d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980571"
---
# <a name="use-bulk-insert-or-openrowsetbulk-to-import-data-to-sql-server"></a>使用 BULK INSERT 或 OPENROWSET(BULK...) 將資料匯入 SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

本文提供一個概觀，說明如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT 陳述式與 INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式，從資料檔案大量匯入資料到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 資料表中。 本文也會描述有關使用 BULK INSERT 和 OPENROWSET(BULK…)，以及使用這些方法從遠端資料來源大量匯入時的安全性考量。

> [!NOTE]
> 當您使用 BULK INSERT 或 OPENROWSET(BULK…) 時，了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本處理模擬的方式相當重要。 如需詳細資訊，請參閱本主題稍後的「安全性考量」。

## <a name="bulk-insert-statement"></a>BULK INSERT 陳述式

BULK INSERT 會從資料檔案將資料載入資料表。 此功能與 **bcp** 命令的 **in** 選項相似，但卻是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序來讀取資料檔案。 如需 BULK INSERT 語法的描述，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。

## <a name="bulk-insert-examples"></a>BULK INSERT 範例

- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)
- [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [大量匯入資料時保留識別值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [指定欄位與資料列結束字元 &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)
- [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)
- [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
- [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)
- [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK...)函式

OPENROWSET BULK 資料列集提供者可透過呼叫 OPENROWSET 函數及指定 BULK 選項加以存取。 OPENROWSET(BULK…) 函數可讓您透過 OLE DB 提供者連接到遠端資料來源 (例如資料檔案)，以存取遠端資料。

若要大量匯入資料，請從 INSERT 陳述式內的 SELECT…FROM 子句呼叫 OPENROWSET(BULK…)。 大量匯入資料的基本語法是：

INSERT ...SELECT * FROM OPENROWSET(BULK...)

當用於 INSERT 陳述式時，OPENROWSET(BULK...) 支援資料表提示。 除了一般的資料表提示 (例如 TABLOCK) 之外，BULK 子句也接受下列特殊化資料表提示：IGNORE_CONSTRAINTS (僅忽略 CHECK 條件約束)、IGNORE_TRIGGERS、KEEPDEFAULTS 及 KEEPIDENTITY。 如需詳細資訊，請參閱[資料表提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)。

如需 BULK 選項其他用法的資訊，請參閱 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)。

## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式 - 範例：

- [大量匯入與匯出 XML 文件的範例 &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [大量匯入資料時保留識別值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [大量匯入期間保留 Null 或使用預設值 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [使用格式檔案大量匯入資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [使用格式檔案略過資料表資料行 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [使用格式檔案略過資料欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [使用格式檔案將資料表資料行對應至資料檔案欄位 &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="security-considerations"></a>安全性考量

如果使用者是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，則會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序帳戶的安全性設定檔。 使用 SQL Server 驗證的登入無法於 Database Engine 外部進行驗證。 因此，一旦使用 SQL Server 驗證的登入起始 BULK INSERT 命令，將會使用 SQL Server 處理序帳戶 (即 SQL Server Database Engine 服務所使用的帳戶) 的安全性內容建立與資料的連接。 

為了能夠成功讀取來源資料，您必須授與 SQL Server Database Engine 所使用的帳戶對來源資料的存取權。 相反地，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者是使用 Windows 驗證登入，則該使用者只能讀取其使用者帳戶可存取的檔案，而與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序的安全性設定檔無關。

例如，有個使用者使用 Windows 驗證登入了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如果這個使用者要用 BULK INSERT 或 OPENROWSET 從資料檔案匯入資料到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，則使用者帳戶必須具有資料檔案的讀取權限。 有了資料檔案的存取權之後，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序沒有權限存取檔案，使用者還是可以將檔案中的資料匯入到資料表。 使用者不需要將檔案存取權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 可以設定為，透過轉送已驗證 Windows 使用者的認證，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體連接到另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 此設置也稱為「模擬」  或「委派」  。 當您使用 BULK INSERT 或 OPENROWSET 時，請務必了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本如何處理使用者模擬的安全性。 使用者模擬允許資料檔案位於和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序或使用者不同的電腦上。 例如，如果位於 **Computer_A** 的使用者可以存取 **Computer_B**上的資料檔案，且已適當設定認證委派，則使用者可以連接到執行於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer_C **上的**執行個體，然後存取 **Computer_B**上的資料檔案，並從該檔案大量匯入資料到 **Computer_C**上的資料表。

## <a name="bulk-importing-to-sql-server-from-a-remote-data-file"></a>從遠端資料檔案大量匯入至 SQL Server

若要使用 BULK INSERT 或 INSERT...SELECT \* FROM OPENROWSET(BULK...) 從另一部電腦大量匯入資料，則必須在兩部電腦之間共用資料檔案。 若要指定共用資料檔案，請使用它的通用命名慣例 (UNC) 名稱，其使用一般格式： **\\\\** <伺服器名稱>  **\\** <共用名稱>  **\\** <路徑>  **\\** <檔案名稱>  。 此外，用來存取資料檔案的帳戶必須擁有在遠端磁碟上讀取檔案所需的權限。

例如，下列 `BULK INSERT` 陳述式會從名為 `SalesOrderDetail` 的資料檔案大量匯入資料到 `AdventureWorks` 資料庫的 `newdata.txt`資料表。 此資料檔案位於 `\dailyorders` 系統上的 `salesforce` 網路共用目錄上的 `computer2`共用資料夾中。

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';
```

> [!NOTE]
> 這個限制並不適用於 **bcp** 公用程式，因為用戶端可以獨立讀取檔案，不受 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 影響。

## <a name="bulk-importing-from-azure-blob-storage"></a>從 Azure Blob 儲存體大量匯入

從 Azure Blob 儲存體匯入且資料不是公用 (匿名存取) 時，請依據使用 [MASTER KEY](../../t-sql/statements/create-master-key-transact-sql.md) 加密的 SAS 金鑰建立 [DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)，然後建立要用於 BULK INSERT 命令中的[外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md)。

### <a name="using-bulk-insert"></a>使用 BULK INSERT

下列範例說明如何使用 BULK INSERT 命令，從建立 SAS 金鑰之 Azure Blob 儲存體位置上的 CSV 檔案載入資料。 Azure Blob 儲存體位置已設定為外部資料來源。 這需要使用在使用者資料庫中以主要金鑰加密的共用存取簽章來進行資料庫範圍認證。

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Azure SQL Database 不支援從 Windows 檔案讀取。

### <a name="using-openrowset"></a>使用 OPENROWSET

下列範例說明如何使用 OPENROWSET 命令，從已建立 SAS 金鑰的 Azure Blob 儲存體位置中 CSV 檔案載入資料。 Azure Blob 儲存體位置已設定為外部資料來源。 這需要使用在使用者資料庫中以主要金鑰加密的共用存取簽章來進行資料庫範圍認證。

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

INSERT INTO achievements with (TABLOCK) (id, description)
SELECT * FROM OPENROWSET(
   BULK  'csv/achievements.csv',
   DATA_SOURCE = 'MyAzureBlobStorage',
   FORMAT ='CSV',
   FORMATFILE='csv/achievements-c.xml',
   FORMATFILE_DATA_SOURCE = 'MyAzureBlobStorage'
    ) AS DataFile;
```

> [!IMPORTANT]
> Azure SQL Database 不支援從 Windows 檔案讀取。

## <a name="see-also"></a>另請參閱

- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [SELECT 子句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)
- [資料的大量匯入及匯出 &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [bcp 公用程式](../../tools/bcp-utility.md)
- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
