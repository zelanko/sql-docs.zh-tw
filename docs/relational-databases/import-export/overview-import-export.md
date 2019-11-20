---
title: 匯入和匯出 SQL Server 和 Azure SQL Database 的資料
ms.date: 10/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: c131954cce8e65cd7f309b59f3780bbd214cb228
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74055935"
---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>匯入和匯出 SQL Server 和 Azure SQL Database 的資料
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
您可以使用各種方法在 SQL Server 和 Azure SQL Database 匯入和匯出資料。 這些方法包括 Transact-SQL 陳述式、命令列工具和精靈。

您也可以匯入和匯出各種不同資料格式的資料。 這些格式包括一般檔案、Excel、主要關聯式資料庫，以及各種雲端服務。

## <a name="methods-for-importing-and-exporting-data"></a>匯入和匯出資料的方法

### <a name="use-transact-sql-statements"></a>使用 Transact-SQL 陳述式
您可以使用 `BULK INSERT` 或 `OPENROWSET(BULK...)` 命令匯入資料。 您通常是在 SQL Server Management Studio (SSMS) 中執行這些命令。 如需詳細資訊，請參閱[使用 BULK INSERT 或 OPENROWSET(BULK...) 匯入大量資料](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

### <a name="use-bcp-from-the-command-prompt"></a>從命令提示字元使用 BCP
您可以使用 BCP 命令列公用程式匯入和匯出資料。 如需詳細資訊，請參閱[使用 bcp 公用程式匯入及匯出大量資料](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

### <a name="use-the-import-flat-file-wizard"></a>使用「匯入一般檔案精靈」
如果您不需要使用「匯入及匯出精靈」和其他工具中的所有設定選項，則可以使用 SQL Server Management Studio (SSMS) 中的**匯入一般檔案精靈**將文字檔匯入 SQL Server。 如需詳細資訊，請參閱下列文章：
- [將一般檔案匯入 SQL 精靈](import-flat-file-wizard.md)
- [What's new in SQL Server Management Studio 17.3](https://blogs.technet.microsoft.com/dataplatforminsider/2017/10/10/whats-new-in-sql-server-management-studio-17-3/) (SQL Server Management Studio 17.3 的新功能)
- [在 SSMS 17.3 中新推出的「匯入一般檔案精靈」簡介](https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-new-Import-Flat-File-Wizard-in-SSMS-173) \(英文\)

### <a name="use-the-sql-server-import-and-export-wizard"></a>使用 SQL Server 匯入和匯出精靈
您可以使用 [SQL Server 匯入和匯出精靈] 從各種不同的來源和目的地匯入資料或匯出資料。 若要使用精靈，您必須安裝 SQL Server Integration Services (SSIS) 或 SQL Server Data Tools (SSDT)。 如需詳細資訊，請參閱[使用 SQL Server 匯入和匯出精靈匯入和匯出資料](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

### <a name="design-your-own-import-or-export"></a>自行設計匯入或匯出
如果您想要設計自訂的資料匯入，您可以使用下列一項功能或服務：
-   SQL Server Integration Services。 如需詳細資訊，請參閱 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。
-   Azure Data Factory。 如需詳細資訊，請參閱 [Azure Data Factory 簡介](https://docs.microsoft.com/azure/data-factory/data-factory-introduction)。

## <a name="data-formats-for-import-and-export"></a>匯入及匯出的資料格式

### <a name="supported-formats"></a>支援的格式

您可以匯入及匯出一般檔案或各種其他檔案格式、關聯式資料庫和雲端服務的資料。 若要深入了解特定工具的這些選項，請參閱下列主題。
-   針對 SQL Server 匯入和匯出精靈，請參閱[使用 SQL Server 匯入和匯出精靈連線至資料來源](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md)。
-   針對 SQL Server Integration Services，請參閱 [Integration Services (SSIS) 連線](../../integration-services/connection-manager/integration-services-ssis-connections.md)。
-   針對 Azure Data factory，請參閱 [Azure Data Factory 連接器](https://docs.microsoft.com/azure/data-factory/data-factory-amazon-redshift-connector)。

### <a name="commonly-used-data-formats"></a>常用的資料格式

一些常用的資料格式有特殊考量和範例。 若要深入了解這些資料格式，請參閱下列主題：
-   針對 Excel，請參閱[從 Excel 匯入](import-data-from-excel-to-sql.md)。
-   針對 JSON，請參閱[匯入 JSON 文件](../json/import-json-documents-into-sql-server.md)。
-   針對 XML，請參閱[匯入及匯出 XML 文件](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)。
-   針對 Azure Blob 儲存體，請參閱[從 Azure Blob 儲存體匯入及匯出](examples-of-bulk-access-to-data-in-azure-blob-storage.md)。

## <a name="next-steps"></a>後續步驟
如果您不確定從何開始匯入或匯出工作，請考慮使用 SQL Server 匯入和匯出精靈。 如需快速簡介，請參閱[開始使用匯入和匯出精靈的簡單範例](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。
