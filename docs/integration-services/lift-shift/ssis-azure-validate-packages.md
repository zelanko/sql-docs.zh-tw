---
title: 驗證部署到 Azure 的 SSIS 套件 | Microsoft Docs
description: 了解 [SSIS 套件部署精靈] 如何檢查套件中是否有已知問題，導致套件無法在 Azure 中如預期般執行。
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 41985e8d39de843c8319ac3ac5622c4cb8b4aa51
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/31/2020
ms.locfileid: "89195134"
---
# <a name="validate-sql-server-integration-services-ssis-packages-deployed-to-azure"></a>驗證部署到 Azure 的 SQL Server Integration Services (SSIS) 套件

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



當您將 SQL Server Integration Services (SSIS) 專案部署到 Azure 伺服器上的 SSIS 目錄 (SSISDB) 時，[套件部署精靈] 會在 [檢閱]  頁面之後新增額外的驗證步驟。 此驗證步驟會檢查專案中的套件，尋找是否存在可能會導致套件無法在 Azure SSIS Integration Runtime 中如期般執行的已知問題。 精靈隨後會在 [驗證]  頁面上顯示任何相關的警告。

> [!IMPORTANT]
> 當您部署 SQL Server Data Tools (SSDT) 17.4 版或更新版本的專案時，就會發生本文所述的驗證。 若要取得最新版的 SSDT，請參閱[下載 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。

如需 [套件部署精靈] 的詳細資訊，請參閱[部署 Integration Services (SSIS) 專案及套件](../packages/deploy-integration-services-ssis-projects-and-packages.md)。

## <a name="validate-connection-managers"></a>驗證連線管理員

此精靈會檢查特定連線管理員，了解其是否具有下列可能導致連線失敗的問題：
- **Windows 驗證**。 若連接字串使用 Windows 驗證，驗證就會產生警告。 Windows 驗證需要其他設定步驟。 如需詳細資訊，請參閱[使用 Windows 驗證連線至資料和檔案共用](ssis-azure-connect-with-windows-auth.md)。
- **檔案路徑**。 若連接字串包含硬式編碼的本機檔案路徑 (例如 `C:\\...`)，驗證就會產生警告。 包含絕對路徑的套件可能會失敗。
- **UNC 路徑**。 若連接字串包含 UNC 路徑，驗證就會產生警告。 包含 UNC 路徑的套件可能會失敗，原因通常是 UNC 路徑需要 Windows 驗證才可存取。
- **主機名稱**。 若伺服器屬性包含主機名稱而非 IP 位址，驗證就會產生警告。 包含主機名稱的套件可能會失敗，原因通常是因為 Azure 虛擬網路需要正確的 DNS 設定來支援 DNS 名稱解析。
- **提供者或驅動程式**。 若提供者或驅動程式不受支援，驗證就會產生警告。 此時僅支援少數的內建提供者與驅動程式。

精靈會對清單中的連線管理員進行下列驗證檢查。

| 連線管理員 | Windows 驗證 | 檔案路徑 | UNC 路徑 | 主機名稱 | 提供者或驅動程式 |
|--------------------|----------|-----------|-----|-----------|-------------------|
| Ado                | âœ“        |           |     | âœ“         | âœ“                 |
| AdoNet             | âœ“        |           |     | âœ“         | âœ“                 |
| 快取              |          | âœ“         | âœ“   |           |                   |
| Excel              |          | âœ“         | âœ“   |           |                   |
| 檔案               |          | âœ“         | âœ“   |           |                   |
| FlatFile           |          | âœ“         | âœ“   |           |                   |
| Ftp                |          |           |     | âœ“         |                   |
| MsOLAP100          |          |           |     | âœ“         | âœ“                 |
| MultiFile          |          | âœ“         | âœ“   |           |                   |
| MultiFlatFile      |          | âœ“         | âœ“   |           |                   |
| OData              | âœ“        |           |     | âœ“         |                   |
| ODBC               | âœ“        |           |     | âœ“         | âœ“                 |
| OleDb              | âœ“        |           |     | âœ“         | âœ“                 |
| SmoServer          | âœ“        |           |     | âœ“         |                   |
| Smtp               | âœ“        |           |     | âœ“         |                   |
| SqlMobile          |          | âœ“         | âœ“   |           |                   |
| Wmi                | âœ“        |           |     |           |                   |
|||||||

## <a name="validate-sources-and-destinations"></a>驗證來源與目的地
不支援下列協力廠商來源與目的地：

-   Attunity 的 Oracle 來源與目的地
-   Attunity 的 Teradata 來源與目的地
-   SAP BW 來源與目的地

## <a name="validate-tasks-and-components"></a>驗證工作與元件

### <a name="execute-process-task"></a>執行處理工作

若命令指向具絕對路徑的本機檔案，或是具 UNC 路徑的檔案，驗證就會產生警告。 這些路徑可能會導致 Azure 執行失敗。

### <a name="script-task-and-script-component"></a>指令碼工作和指令碼元件

若套件包含參考或呼叫不受支援之組件的指令碼工作或指令碼元件，驗證就會產生警告。 這些參考或呼叫可能會導致執行失敗。

### <a name="other-components"></a>其他元件

在 HDFS 目的地與 Azure Data Lake Store 目的地中不支援 Orc 格式。

## <a name="next-steps"></a>後續步驟
若要了解如何在 Azure 上排程套件執行，請參閱[在 Azure 中排程 SSIS 套件](ssis-azure-schedule-packages.md)。
