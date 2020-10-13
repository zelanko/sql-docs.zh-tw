---
title: 將 Excel 中的資料匯入到 SQL | Microsoft Docs
description: 本文描述將 Excel 資料匯入 SQL Server 或 Azure SQL Database 的方法。 某些使用單一步驟，其他則需要中繼文字檔。
ms.custom: sqlfreshmay19
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6b299248e1bd953109d72e4536a4d520ccd942d7
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868762"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>將 Excel 中的資料匯入到 SQL Server 或 Azure SQL Database

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

有數種方式可以將 Excel 檔案中的資料匯入到 SQL Server 或 Azure SQL Database。 某些方法可讓您只執行一個步驟，便能直接從 Excel 檔案匯入資料；其他方法會要求先將 Excel 資料匯出成文字 (CSV 檔案) 才可匯入這些文字。 本文摘要說明常用的方法，並提供連結，為您提供更詳細的資訊。

## <a name="list-of-methods"></a>方法清單

您可以使用下列工具來從 Excel 匯入資料：

| 先匯出成文字 (SQL Server 和 SQL Database) | 直接從 Excel 匯入 (僅限 SQL Server 內部部署) |
| :------------------------------------------------- |:------------------------------------------------- |
| [匯入一般檔案精靈](#import-wiz)             |[SQL Server 匯入和匯出精靈](#wiz)        |
| [BULK INSERT](#bulk-insert) 陳述式              |[SQL Server Integration Services (SSIS)](#ssis)    |
| [BCP](#bcp)                                        |[OPENROWSET](#openrowset) 函數 <br>            |
| [複製精靈 (Azure Data Factory)](#adf-wiz)       |                                                   |
| [Azure Data Factory](#adf)                         |                                                   |
| &nbsp; | &nbsp; |

如果想要從 Excel 活頁簿匯入多個工作表，則通常必須針對每個工作表執行一次這些工具的任何一個。

針對複雜工具和服務 (例如 SSIS 或 Azure Data Factory) 的完整描述不在此清單的涵蓋範圍內。 若要深入了解您感興趣的解決方案，請遵循提供的連結。

> [!IMPORTANT]
> 如需連接至 Excel 檔案，以及將資料從 Excel 檔案載入或載入至 Excel 檔案的限制與已知問題的詳細資訊，請參閱[使用 SQL Server Integration Services (SSIS) 將資料從 Excel 載入或載入至 Excel](../../integration-services/load-data-to-from-excel-with-ssis.md)。

如果您未安裝 SQL Server，或您有 SQL Server 但未安裝 SQL Server Management Studio，請參閱 [下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="sql-server-import-and-export-wizard"></a><a name="wiz"></a> SQL Server 匯入和匯出精靈

逐步執行 [SQL Server 匯入和匯出精靈] 的頁面，以從 Excel 檔案直接匯入資料。 您也可以將設定儲存為 SQL Server Integration Services (SSIS) 套件，以便日後自訂及重複使用。

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。

2. 展開 **[資料庫]** 。
3. 以滑鼠右鍵按一下資料庫。
4. 指向 [工作]  。
5. 按一下下列其中一個選項。

  - **匯入資料**
  - **匯出資料**

    ![啟動精靈 (SSMS)](../../integration-services/import-export-data/media/start-wizard-ssms.jpg)

![連線至 Excel 資料來源](media/excel-connection.png)

如需使用精靈從 Excel 匯入至 SQL Server 的範例，請參閱[透過這個匯入和匯出精靈的簡單範例來開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

若要了解啟動「匯入和匯出精靈」的其他方式，請參閱[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。

## <a name="sql-server-integration-services-ssis"></a><a name="ssis"></a> SQL Server Integration Services (SSIS)

如果您熟悉 SSIS 且不想執行 SQL Server 匯入和匯出精靈，請建立在資料流程中使用 Excel 來源和 SQL Server 目的地的 SSIS 套件。

如需這些 SSIS 元件的詳細資訊，請參閱下列主題：

- [Excel 來源](../../integration-services/data-flow/excel-source.md)
- [SQL Server 目的地](../../integration-services/data-flow/sql-server-destination.md)

若要開始學習如何建置 SSIS 套件，請參閱[如何建立 ETL 套件](../../integration-services/ssis-how-to-create-an-etl-package.md)的教學課程。

![資料流程中的元件](media/excel-to-sql-data-flow.png)

## <a name="openrowset-and-linked-servers"></a><a name="openrowset"></a> OPENROWSET 和連結的伺服器

> [!IMPORTANT]
> 在 Azure SQL Database 中，您無法直接從 Excel 匯入。 您必須先將資料匯出成文字 (CSV) 檔案。 如需範例，請參閱[範例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

> [!NOTE]
> 連接至 Excel 資料來源的 ACE 提供者 (先前稱為 Jet 提供者) 是供互動式用戶端使用。 如果您在 SQL 伺服器上使用 ACE 提供者 (特別是在自動化程序或平行執行的程序中)，可能會看到非預期的結果。

### <a name="distributed-queries"></a>分散式查詢

使用 Transact-SQL `OPENROWSET` 或 `OPENDATASOURCE` 函式，直接從 Excel 將資料匯入至 SQL Server。 此使用方式稱為「分散式查詢」  。

> [!IMPORTANT]
> 在 Azure SQL Database 中，您無法直接從 Excel 匯入。 您必須先將資料匯出成測試 (CSV) 檔案。 如需範例，請參閱[範例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

在您可以執行分散式查詢之前，必須啟用 `ad hoc distributed queries` 伺服器設定選項，如下列範例所示。 如需詳細資訊，請參閱[特定分散式查詢伺服器設定選項](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)。

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

下列程式碼範例使用 `Sheet1`，將資料從 Excel `OPENROWSET` 工作表匯入至新的資料庫資料表。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=C:\Temp\Data.xlsx', [Sheet1$]);
GO
```

以下是使用 `OPENDATASOURCE` 的相同範例。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=C:\Temp\Data.xlsx;Extended Properties=Excel 12.0')...[Sheet1$];
GO
```

若要將匯入的資料「附加」  到「現有」  的資料表，而不建立新的資料表，請使用 `INSERT INTO ... SELECT ... FROM ...` 語法，而不是上述範例中使用的 `SELECT ... INTO ... FROM ...` 語法。

若要查詢 Excel 資料但不進行匯入，請直接使用標準 `SELECT ... FROM ...` 語法。

如需分散式查詢的詳細資訊，請參閱下列主題：

- [分散式查詢](/previous-versions/sql/sql-server-2008-r2/ms188721(v=sql.105)) (SQL Server 2016 仍支援分散式查詢，但適用於此功能的文件並未更新。)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
- [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>連結的伺服器

您也可以將 SQL Server 到 Excel 檔案的持續連線設定為「連結的伺服器」  。 下列範例會將資料從現有 Excel 連結伺服器 `EXCELLINK` 的 `Data` 工作表匯入至名為 `Data_ls` 的新 SQL Server 資料庫資料表。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

您可以從 SQL Server Management Studio，或是執行系統預存程序 `sp_addlinkedserver` (如下列範例所示) 來建立連結的伺服器。

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'C:\Temp\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

如需連結的伺服器的詳細資訊，請參閱下列主題：

- [建立連結的伺服器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
- [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

如需連結的伺服器和分散式查詢的更多範例及詳細資訊，請參閱下列主題：

- [如何搭配使用 Excel 以及 SQL Server 連結伺服器和分散式查詢](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
- [如何將 Excel 中的資料匯入到 SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a><a name="prereq"></a> 必要條件：將 Excel 資料儲存為文字

若要使用此頁面所描述的剩餘方法 (BULK INSERT 陳述式、BCP 工具或 Azure Data Factory)，您必須先將 Excel 資料匯出為文字檔。

在 Excel 中，選取 [檔案 | 另存新檔]  ，然後選取 [文字檔 (Tab 字元分隔) (\*.txt)]  或 [CSV (逗號分隔) (\*.csv)]  作為目的地檔案類型。

如果您想要從活頁簿匯出多個工作表，請選取每個工作表，然後重複此程序。 **另存新檔**命令只會匯出使用中工作表。

> [!TIP]
> 若要取得資料匯入工具的最佳結果，請儲存僅包含資料行標題和包含資料之資料列的工作表。 如果儲存的資料包含頁面標題、空白行、註解和其他內容，您稍後在匯入資料時可能會看到非預期的結果。

## <a name="the-import-flat-file-wizard"></a><a name="import-wiz"></a> 匯入一般檔案精靈

逐步設定「匯入一檔案精靈」的每個頁面，匯入儲存為文字檔的資料。

如先前[必要條件](#prereq)一節中所述，您必須將 Excel 資料匯出成文字，才能使用「匯入一般檔案精靈」將它匯入。

如需「匯入一般檔案精靈」的詳細資訊，請參閱[將一般檔案匯入 SQL 精靈](import-flat-file-wizard.md)。

## <a name="bulk-insert-command"></a><a name="bulk-insert"></a> BULK INSERT 命令

`BULK INSERT` 是您可從 SQL Server Management Studio 執行的 Transact-SQL 命令。 下列範例會將來自 `Data.csv` 逗號分隔檔案的資料載入至現有資料庫資料表。

如先前[必要條件](#prereq)一節中所述，您必須將 Excel 資料匯出成文字，才能使用 BULK INSERT 將它匯入。 BULK INSERT 無法直接讀取 Excel 檔案。 您可以使用 BULK INSERT 命令匯入儲存在本機或 Azure Blob 儲存體中的 CSV 檔案。

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'C:\Temp\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

如需 SQL Server 和 SQL Database 的詳細資訊和範例，請參閱下列主題：

- [使用 BULK INSERT 或 OPENROWSET(BULK...) 匯入大量資料](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a><a name="bcp"></a> BCP 工具

BCP 是您從命令提示字元執行的程式。 下列範例會將來自 `Data.csv` 逗號分隔檔案的資料載入至現有 `Data_bcp` 資料庫資料表。

如先前[必要條件](#prereq)一節中所述，您必須將 Excel 資料匯出成文字，才能使用 BCP 將它匯入。 BCP 無法直接讀取 Excel 檔案。 用於從儲存在本機儲存體的測試 (CSV) 檔案匯入至 SQL Server 或 SQL Database。

> [!IMPORTANT]
> 針對儲存在 Azure Blob 儲存體中的文字 (CSV) 檔案，請使用 BULK INSERT 或 OPENROWSET。 如需範例，請參閱[範例](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

```console
bcp.exe ImportFromExcel..Data_bcp in "C:\Temp\data.csv" -T -c -t ,
```

如需 BCP 的詳細資訊，請參閱下列主題：

- [使用 bcp 公用程式匯入及匯出大量資料](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
- [bcp 公用程式](../../tools/bcp-utility.md)
- [準備大量匯出或匯入的資料](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a><a name="adf-wiz"></a> 複製精靈 (Azure Data Factory)

逐步設定「Azure Data Factory 複製精靈」的每個頁面，匯入儲存為文字檔的資料。

如先前[必要條件](#prereq)一節中所述，您必須將 Excel 資料匯出成文字，才能使用 Azure Data Factory 將它匯入。 Data Factory 無法直接讀取 Excel 檔案。

如需 [複製精靈] 的詳細資訊，請參閱下列主題：

- [Data Factory 複製精靈](/azure/data-factory/data-factory-azure-copy-wizard)
- [教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線](/azure/data-factory/data-factory-copy-data-wizard-tutorial)。

## <a name="azure-data-factory"></a><a name="adf"></a> Azure Data Factory

如果您熟悉 Azure Data Factory，且不想執行 [複製精靈]，請建立具有 [複製] 活動的管線，以從文字檔複製至 SQL Server 或 Azure SQL Database。

如先前[必要條件](#prereq)一節中所述，您必須將 Excel 資料匯出成文字，才能使用 Azure Data Factory 將它匯入。 Data Factory 無法直接讀取 Excel 檔案。

如需使用這些 Data Factory 來源與接收的詳細資訊，請參閱下列主題：

- [檔案系統](/azure/data-factory/data-factory-onprem-file-system-connector)
- [SQL Server](/azure/data-factory/data-factory-sqlserver-connector)
- [Azure SQL Database](/azure/data-factory/data-factory-azure-sql-connector)

若要開始學習如何使用 Azure Data Factory 複製資料，請參閱下列主題：

- [使用複製活動來移動資料](/azure/data-factory/data-factory-data-movement-activities)
- [教學課程：使用 Azure 入口網站建立具有複製活動的管線](/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="common-errors"></a>常見錯誤

### <a name="microsoftaceoledb120-has-not-been-registered"></a>Microsoft.ACE.OLEDB.12.0 尚未註冊

此錯誤的發生原因為未安裝 OLEDB 提供者。 請從 [Microsoft Access Database Engine 2010 可轉散發套件](https://www.microsoft.com/download/details.aspx?id=13255)安裝它。 如果 Windows 和 SQL Server 都是 64 位元，請務必安裝 64 位元版本。

完整錯誤如下：

```
Msg 7403, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" has not been registered.
```

### <a name="cannot-create-an-instance-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>無法建立連結伺服器 "(null)" OLE DB 提供者 "Microsoft.ACE.OLEDB.12.0" 的執行個體

這表示 Microsoft OLEDB 並未正確設定。 執行下列 Transact-SQL 程式碼來解決此問題：

```sql
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'AllowInProcess', 1
EXEC sp_MSset_oledb_prop N'Microsoft.ACE.OLEDB.12.0', N'DynamicParameters', 1
```

完整錯誤如下：

```
Msg 7302, Level 16, State 1, Line 3
Cannot create an instance of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

### <a name="the-32-bit-ole-db-provider-microsoftaceoledb120-cannot-be-loaded-in-process-on-a-64-bit-sql-server"></a>64 位元 SQL Server 無法以同處理序方式載入 32 位元 OLE DB 提供者 "Microsoft.ACE.OLEDB.12.0"。

使用 64 位元 SQL Server 安裝 32 位元版本的 OLD DB 提供者時，即會發生此錯誤。 若要解決此問題，請解除安裝 32 位元版本，並改為安裝 64 位元版本的 OLE DB 提供者。

完整錯誤如下：

```
Msg 7438, Level 16, State 1, Line 3
The 32-bit OLE DB provider "Microsoft.ACE.OLEDB.12.0" cannot be loaded in-process on a 64-bit SQL Server.
```

### <a name="the-ole-db-provider-microsoftaceoledb120-for-linked-server-null-reported-an-error-the-provider-did-not-give-any-information-about-the-error"></a>連結伺服器 "(null)" 的 OLE DB 提供者 "Microsoft.ACE.OLEDB.12.0" 報告了錯誤。 提供者並未給予任何關於錯誤的資訊

### <a name="cannot-initialize-the-data-source-object-of-ole-db-provider-microsoftaceoledb120-for-linked-server-null"></a>無法初始化連結伺服器 "(null)" OLE DB 提供者 "Microsoft.ACE.OLEDB.12.0" 的資料來源物件

這兩個錯誤通常表示在 SQL Server 處理序和檔案之間發生權限問題。 請確定執行 SQL Server 服務的帳戶具有檔案的完整存取權限。 我們建議您不要嘗試從桌面匯入檔案。

完整錯誤如下：

```
Msg 7399, Level 16, State 1, Line 3
The OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)" reported an error. The provider did not give any information about the error.
```

```
Msg 7303, Level 16, State 1, Line 3
Cannot initialize the data source object of OLE DB provider "Microsoft.ACE.OLEDB.12.0" for linked server "(null)".
```

## <a name="see-also"></a>另請參閱

[使用 SQL Server Integration Services (SSIS) 從 Excel 匯入資料，或將資料匯出至 Excel](../../integration-services/load-data-to-from-excel-with-ssis.md)