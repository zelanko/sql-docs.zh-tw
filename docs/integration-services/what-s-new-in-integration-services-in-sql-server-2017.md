---
title: SQL Server 2017 中的 Integration Services 新功能 | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2baea8e71a3730a100eda8971ad70a28f1a97773
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296462"
---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>SQL Server 2017 中的 Integration Services 新功能

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


本主題描述 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中已新增或更新的功能。

> [!NOTE]
> SQL Server 2017 也包含 SQL Server 2016 的功能以及 SQL Server 2016 更新中新增的功能。 如需 SQL Server 2016 的 SSIS 新功能資訊，請參閱 [SQL Server 2016 的 Integration Services 新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="highlights-of-this-release"></a>這版的重點

以下是 SQL Server 2017 中 Integration Services 的最重要新功能。

-   **擴增**。更輕鬆地將 SSIS 套件執行散發到多個背景工作電腦，以及透過單一主要電腦管理執行和背景工作。 如需詳細資訊，請參閱 [Integration Services 擴增](../integration-services/scale-out/integration-services-ssis-scale-out.md)。

-   **Linux 上的 Integration Services**。 在 Linux 電腦上執行 SSIS 套件。 如需詳細資訊，請參閱[使用 SSIS 在 Linux 上擷取、轉換和載入資料](../linux/sql-server-linux-migrate-ssis.md)。

-   **連線能力改善**。 使用更新的 OData 元件連線至 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 摘要。 

## <a name="new-in-azure-data-factory"></a>Azure Data Factory 的新功能

使用 2017 年 9 月 Azure Data Factory 第 2 版的公開預覽，您現在可以執行下列動作：
-   將套件部署至 Azure SQL Database 上的 SSIS 目錄資料庫 (SSISDB)。
-   在 Azure-SSIS Integration Runtime (即 Azure Data Factory 第 2 版的元件) 上執行部署至 Azure 的套件。

如需詳細資訊，請參閱[將 SQL Server Integration Services 工作負載隨即轉移至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

這些新功能需要 SQL Server Data Tools (SSDT) 17.2 版或更新版本，但不需要 SQL Server 2017 或 SQL Server 2016。 當您將套件部署至 Azure 時，[套件部署精靈] 一律會將套件升級至最新套件格式。

## <a name="new-in-the-azure-feature-pack"></a>Azure Feature Pack 的新功能

除了 SQL Server 中的連線能力改善之外，Integration Services Feature Pack for Azure 還新增對 Azure Data Lake Store 的支援。 如需詳細資訊，請參閱部落格文章：[新 Azure Feature Pack 版本加強 ADLS 連線能力](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/)。 另請參閱 [Azure Feature Pack for Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md)。

## <a name="new-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 的新功能

您現在可以透過 Visual Studio 2017 或 Visual Studio 2015 中的 2017 開發將目標設為 SQL Server 2012 版的 SSIS 專案和套件。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SQL Server 2017 RC1 的 SSIS 新功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS 擴增的新功能和變更的功能

-   擴增主機現在支援高可用性。 您可以針對裝載擴增主機服務的伺服器，啟用 AlwaysOn for SSISDB 並設定 Windows Server 容錯移轉叢集。 將這項變更套用至擴增主機，即可避免單一失敗點，以及提供整個擴增部署的高可用性。
-   擴增背景工作中執行記錄的容錯移轉處理已獲得改善。 如果擴增背景工作意外停止，則會將執行記錄保存到本機磁碟。 稍後，背景工作重新啟動時，會重新載入保存記錄，並繼續將它們儲存至 SSISDB。
-   為了一致性和可讀性，預存程序 **[catalog].[create_execution]** 的參數 *runincluster* 已重新命名為 *runinscaleout*。 這項參數名稱變更的影響如下：
    -   如果您的現有指令碼可在擴增中執行套件，則必須將參數名稱從 *runincluster* 變更為 *runinscaleout*，以確保這些指令碼在 RC1 中正常運作。
    -   SQL Server Management Studio (SSMS) 17.1 和舊版本無法在 RC1 的擴增中觸發套件執行。 錯誤訊息為：「 *@runincluster* 不是程序 **create_execution** 的參數。」 SSMS 的下一個版本 17.2 版中將會修正此問題。 SSMS 17.2 版和更新版本支援擴增中的新參數名稱和套件執行。在 SSMS 17.2 版可用之前，作為因應措施，您可以使用現有的 SSMS 版本來產生套件執行指令碼，然後將指令碼中的 *runincluster* 參數名稱變更為 *runinscaleout*，然後執行此指令碼。
-   SSIS 目錄有新的全域屬性，可指定執行 SSIS 套件的預設模式。 當您呼叫 *runinscaleout* 參數設定為 Null 的 **[catalog].[create_execution]** 預存程序時，可以使用這個新屬性。 此模式也適用於 SSIS SQL Agent 作業。 您可以在 SSMS 中 SSISDB 節點的 [屬性] 對話方塊中，或使用下列命令，來設定新的全域屬性：
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>SQL Server 2017 CTP 2.1 的 SSIS 新增功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>SSIS 擴增的新功能和變更的功能

-   在擴增中觸發執行時，您現在可以使用 **Use32BitRuntime** 參數。
-   已改善擴增中套件執行的 SSISDB 記錄效能。 事件訊息和訊息內容記錄現在會以批次模式寫入至 SSISDB，而非逐一寫入。 以下是這項改善的一些其他注意事項：        
    - SQL Server Management Studio (SSMS) 目前版本中的某些報表，現在不會針對擴增中的執行顯示這些記錄。預期下一版的 SSMS 將支援它們。 受影響的報表包含 [所有連線]  報表、[錯誤內容]  報表，以及 [Integration Service 儀表板] 中的 [連線資訊]  區段。
    - 已新增資料行 **event_message_guid**。 在擴增中查詢這些執行記錄時，請使用此資料行來聯結 [catalog].[event_message_context] 檢視與 [catalog].[event_messages] 檢視，而非使用 **event_message_id**。
-   若要取得 SSIS 擴增的管理應用程式，請[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 或更新版本。

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>SQL Server 2017 CTP 2.0 的 SSIS 新功能

SQL Server 2017 CTP 2.0 沒有任何新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>SQL Server 2017 CTP 1.4 的 SSIS 新功能

SQL Server 2017 CTP 1.4 沒有任何新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>SQL Server 2017 CTP 1.3 的 SSIS 新功能

SQL Server 2017 CTP 1.3 沒有任何新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>SQL Server 2017 CTP 1.2 的 SSIS 新功能

SQL Server 2017 CTP 1.2 沒有任何新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>SQL Server 2017 CTP 1.1 的 SSIS 新功能

SQL Server 2017 CTP 1.1 沒有任何新 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SQL Server 2017 CTP 1.0 的 SSIS 新功能

### <a name="scale-out-for-ssis"></a>SSIS 擴增

擴增功能讓 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 更容易在多部電腦上執行。 
   
安裝擴增主機和背景工作之後，封裝即可發佈到不同的背景工作自動執行。 如果執行意外終止，它會自動重試。 而且，所有執行和背景工作都可以使用主機集中管理。
   
如需詳細資訊，請參閱 [Integration Services 擴增](../integration-services/scale-out/integration-services-ssis-scale-out.md)。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 資源的支援

OData 來源和 OData 連接管理員現在支援連接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 摘要。

