---
title: "匯入和匯出 SQL Server 和 Azure SQL Database 的資料 | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3c41be0642b13b63367c5601b716b506808472e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/14/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>匯入和匯出 SQL Server 和 Azure SQL Database 的資料
您可以使用各種方法在 SQL Server 和 Azure SQL Database 匯入和匯出資料。 這些方法包括 Transact-SQL 陳述式、命令列工具和精靈。

您也可以匯入和匯出各種不同資料格式的資料。 這些格式包括一般檔案、Excel、主要關聯式資料庫，以及各種雲端服務。

## <a name="methods-for-importing-and-exporting-data"></a>匯入和匯出資料的方法

### <a name="use-transact-sql-statements"></a>使用 Transact-SQL 陳述式
您可以使用 `BULK INSERT` 或 `OPENROWSET(BULK...)` 命令匯入資料。 您通常是在 SQL Server Management Studio (SSMS) 中執行這些命令。 如需詳細資訊，請參閱[使用 BULK INSERT 或 OPENROWSET(BULK...) 匯入大量資料](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

### <a name="use-bcp-from-the-command-prompt"></a>從命令提示字元使用 BCP
您可以使用 BCP 命令列公用程式匯入和匯出資料。 如需詳細資訊，請參閱[使用 bcp 公用程式匯入及匯出大量資料](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)。

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
-   針對 Azure Data factory，請參閱 [Azure Data Factory 連接器](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector)。

### <a name="commonly-used-data-formats"></a>常用的資料格式

一些常用的資料格式有特殊考量和範例。 若要深入了解這些資料格式，請參閱下列主題：
-   針對 Excel，請參閱[從 Excel 匯入](import-data-from-excel-to-sql.md)。
-   針對 JSON，請參閱[匯入 JSON 文件](../json/import-json-documents-into-sql-server.md)。
-   針對 XML，請參閱[匯入及匯出 XML 文件](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)。
-   針對 Azure Blob 儲存體，請參閱[從 Azure Blob 儲存體匯入及匯出](examples-of-bulk-access-to-data-in-azure-blob-storage.md)。

## <a name="next-steps"></a>後續的步驟
如果您不確定從何開始匯入或匯出工作，請考慮使用 SQL Server 匯入和匯出精靈。 如需快速簡介，請參閱[開始使用匯入和匯出精靈的簡單範例](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。

