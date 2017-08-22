---
title: "將 Excel 中的資料匯入到 SQL | Microsoft Docs"
ms.custom: 
ms.date: 08/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: ab792aed71ab2e7837da9cf0073d4ff191ce5184
ms.openlocfilehash: ce462c238c81a4a9fc82869a856ac13e9f112aee
ms.contentlocale: zh-tw
ms.lasthandoff: 08/05/2017

---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>將 Excel 中的資料匯入到 SQL Server 或 Azure SQL Database
有數種方式可以將 Excel 檔案中的資料匯入到 SQL Server 或 Azure SQL Database。 本文摘要說明所有這些選項，並提供更詳細指示的連結。
-   您可以使用下列其中一種工具，透過單一步驟將資料從 Excel 匯入至 SQL：
    -   SQL Server 匯入和匯出精靈
    -   SQL Server Integration Services (SSIS)
    -   OPENROWSET 函式
-   您可以將資料儲存為文字，然後使用下列其中一種工具，透過兩個步驟來匯入資料：
    -   BULK INSERT 陳述式
    -   BCP
    -   Azure Data Factory

> [!IMPORTANT]
> 針對複雜工具和服務 (例如 SSIS 或 Azure Data Factory) 的完整說明，不在此概觀的涵蓋範圍內。 若要深入了解您感興趣的解決方案，請遵循所提供的連結以取得詳細資訊。

## <a name="sql-server-import-and-export-wizard"></a>SQL Server 匯入和匯出精靈

逐步執行 [SQL Server 匯入和匯出精靈] 的頁面，以從 Excel 檔案直接匯入資料。 您也可以將匯入/匯出設定儲存為 SQL Server Integration Services (SSIS) 套件，以便自訂及重複使用。

![連線至 Excel 資料來源](media/excel-connection.png)

如需使用精靈從 Excel 匯入至 SQL Server 的範例，請參閱[透過這個匯入和匯出精靈的簡單範例來開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

如果您熟悉 SSIS 且不想執行 SQL Server 匯入和匯出精靈，請建立在資料流程中使用 Excel 來源和 SQL Server 目的地的 SSIS 套件。

![資料流程中的元件](media/excel-to-sql-data-flow.png)

如需這些 SSIS 元件的詳細資訊，請參閱下列主題：
-   [Excel 來源](../../integration-services/data-flow/excel-source.md)
-   [SQL Server 目的地](../../integration-services/data-flow/sql-server-destination.md)

若要開始學習如何建置 SSIS 套件，請參閱[如何建立 ETL 套件](../../integration-services/ssis-how-to-create-an-etl-package.md)的教學課程。

## <a name="openrowset-and-linked-servers"></a>OPENROWSET 和連結的伺服器
> [!NOTE]
> 連接至 Excel 資料來源的 ACE 提供者 (先前稱為 Jet 提供者) 是供互動式用戶端使用。 如果您在伺服器上使用 ACE 提供者 (特別是在自動化程序或平行執行的程序中)，可能會看到非預期的結果。

### <a name="distributed-queries"></a>分散式查詢

使用 Transact-SQL `OPENROWSET` 或 `OPENDATASOURCE` 函式，直接從 Excel 檔案匯入資料。 此使用方式稱為「分散式查詢」。

在您可以執行分散式查詢之前，必須啟用 `ad hoc distributed queries` 伺服器設定選項，如下列範例所示。 如需詳細資訊，請參閱[特定分散式查詢伺服器設定選項](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md)。

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

下列程式碼範例使用 `Data`，將資料從 Excel `OPENROWSET` 工作表匯入至新的資料庫資料表。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

以下是使用 `OPENDATASOURCE` 的相同範例。

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

若要將匯入的資料「附加」到「現有」的資料表，而不建立新的資料表，請使用 `INSERT INTO ... SELECT ... FROM ...` 語法，而不是上述範例中使用的 `SELECT ... INTO ... FROM ...` 語法。

若要查詢 Excel 資料但不進行匯入，請直接使用標準 `SELECT ... FROM ...` 語法。

如需分散式查詢的詳細資訊，請參閱下列主題：
-   [分散式查詢](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx)。 (SQL Server 2016 仍支援分散式查詢，但針對此功能的文件尚未更新)。
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>連結的伺服器

您也可以將針對 Excel 檔案的持續連線設定為「連結的伺服器」。 下列範例會將資料從現有 Excel 連結的伺服器 `EXCELLINK` 的 `Data` 工作表匯入至名為 `Data_ls` 的新資料庫資料表。

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
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

如需連結的伺服器的詳細資訊，請參閱下列主題：
-   [建立連結的伺服器](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

如需連結的伺服器和分散式查詢的更多範例及詳細資訊，請參閱下列主題：
-   [如何搭配使用 Excel 以及 SQL Server 連結伺服器和分散式查詢](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries)
-   [如何將 Excel 中的資料匯入到 SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prerequisite---save-excel-data-as-text"></a>必要條件：將 Excel 資料儲存為文字
若要使用此頁面所描述的剩餘方法 (BULK INSERT 陳述式、BCP 工具或 Azure Data Factory)，您必須先將 Excel 資料匯出為文字檔。

在 Excel 中，選取 [檔案 | 另存新檔]，然後選取 [文字檔 (Tab 字元分隔) (\*.txt)] 或 [CSV (逗號分隔) (\*.csv)] 作為目的地檔案類型。

> [!TIP]
> 若要取得資料匯入工具的最佳結果，請儲存僅包含資料行標題和包含資料之資料列的工作表。 如果儲存的資料包含頁面標題、空白行、註解和其他內容，您稍後在匯入資料時可能會看到非預期的結果。

## <a name="bulk-insert-command"></a>BULK INSERT 命令

`BULK INSERT` 是您可從 SQL Server Management Studio 執行的 Transact-SQL 命令。 下列範例會將來自 `Data.csv` 逗號分隔檔案的資料載入至現有資料庫資料表。

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

如需詳細資訊，請參閱下列主題：
-   [使用 BULK INSERT 或 OPENROWSET(BULK...) 匯入大量資料](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp-tool"></a>BCP 工具

BCP 是您從命令提示字元執行的程式。 下列範例會將來自 `Data.csv` 逗號分隔檔案的資料載入至現有 `Data_bcp` 資料庫資料表。

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

如需 BCP 的詳細資訊，請參閱下列主題：
-   [使用 bcp 公用程式匯入及匯出大量資料](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [bcp 公用程式](../../tools/bcp-utility.md)
-   [準備大量匯出或匯入的資料](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="copy-wizard-azure-data-factory"></a>複製精靈 (Azure Data Factory)
透過 [複製精靈] 的頁面，匯入儲存為文字檔的資料。

如需 [複製精靈] 的詳細資訊，請參閱下列主題：
-   [Data Factory 複製精靈](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial)。

## <a name="azure-data-factory"></a>Azure Data Factory
如果您熟悉 Azure Data Factory，且不想執行 [複製精靈]，請建立具有 [複製] 活動的管線，以從文字檔複製至 SQL Server 或 Azure SQL Database。

如需使用這些 Data Factory 來源與接收的詳細資訊，請參閱下列主題：
-   [檔案系統](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [[SQL Server]](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Azure SQL Database](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

若要開始學習如何使用 Azure Data Factory 複製資料，請參閱下列主題：
-   [使用複製活動來移動資料](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [教學課程：使用 Azure 入口網站建立具有複製活動的管線](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="next-steps"></a>後續的步驟

若要深入了解您感興趣的解決方案，請遵循所提供的連結以取得詳細資訊。

