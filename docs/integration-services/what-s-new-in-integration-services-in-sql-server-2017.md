---
title: "什麼 &#39; 在 2017年的 SQL Server Integration Services 中的新 s |Microsoft 文件"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 63aba0f64bc63a3a86e5aa07245375938acdf6e4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/29/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>什麼 & #39 的新 SQL Server 2017 中的 Integration Services
本主題說明 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中已新增或更新的功能。

>   [!NOTE]
> SQL Server 2017 也包含 SQL Server 2016 的功能以及 SQL Server 2016 更新中加入的功能。 如需 SQL Server 2016 的 SSIS 新功能資訊，請參閱 [SQL Server 2016 的 Integration Services 新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="highlights-of-this-release"></a>此版本中的反白顯示

以下是最重要的新功能的 SQL Server 2017 中的 Integration Services。

-   **向外延展**。將 SSIS 封裝執行更輕鬆地分散到多個背景工作電腦，以及管理執行和背景工作從單一的主要電腦。 如需詳細資訊，請參閱[Integration Services 向外](../integration-services/scale-out/integration-services-ssis-scale-out.md)。

-   **在 Linux 上的 integration Services**。 在 Linux 電腦上執行 SSIS 封裝。 如需詳細資訊，請參閱[擷取、 轉換及載入資料，SSIS 與 Linux 上的](../linux/sql-server-linux-migrate-ssis.md)。

-   **改善連線性**。 連接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online OData 摘要與更新的 OData 元件。 

## <a name="new-in-azure-data-factory"></a>Azure Data Factory 的新功能

Azure Data Factory 2017 年 9 月的第 2 版的公用預覽，您現在可以執行下列動作：
-   將封裝部署到 Azure SQL Database 上 SSIS 目錄資料庫 (SSISDB)。
-   執行封裝部署至 Azure 上 Azure SSIS 整合執行階段，Azure Data Factory 第 2 版的元件。

如需詳細資訊，請參閱[增益和 shift SQL Server Integration Services 工作負載至雲端](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)。

這些新功能需要 SQL Server Data Tools (SSDT) 版本 17.2 或更新版本，但不是需要 SQL Server 2017 或 SQL Server 2016。 當您將封裝部署至 Azure 時，套件部署精靈 」 一律為最新的封裝格式升級的封裝。

## <a name="new-in-the-azure-feature-pack"></a>新的 Azure Feature pack

除了 SQL Server 的連線能力增強功能，Integration Services 功能套件，azure 已新增對 Azure 資料湖存放區支援。 如需詳細資訊，請參閱部落格文章[新 Azure 功能套件版本加強 ADLS 連線](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/)。 另請參閱[Azure Feature Pack for Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md)。

## <a name="new-in-sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT) 的新功能

您現在可以開發 SSIS 專案和封裝的 SQL Server 版本 2012年或 Visual Studio 2015 中 Visual Studio 2017 2017年透過目標。 如需詳細資訊，請參閱[下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)。

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SSIS SQL Server 2017 RC1 中的新功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在標尺出適用於 SSIS 的新增和變更功能

-   相應放大主機現在支援高可用性。 您可以針對 SSISDB 啟用 Alwayson，並設定 Windows Server 容錯移轉叢集的伺服器主控標尺出主機服務。 藉由套用到標尺出 Master 的這項變更，您可以避免單一失敗點，並提供整個向外延展部署的高可用性。
-   相應放大背景工作中執行記錄的容錯移轉處理已獲得改善。 執行記錄會保存到本機磁碟，萬一標尺出背景工作意外停止。 稍後，背景工作重新啟動時，它會重新載入保存記錄檔，會繼續將它們儲存至 SSISDB。
-   為了一致性和可讀性，預存程序 **[catalog].[create_execution]** 的參數 *runincluster* 已重新命名為 *runinscaleout*。 這項變更的參數名稱具有下列影響：
    -   如果您有現有的指令碼，以向外執行封裝時，您必須變更參數名稱，從*runincluster*至*runinscaleout*以便在 RC1 中工作的指令碼。
    -   SQL Server Management Studio (SSMS) 17.1 和更早版本，所以無法觸發在 RC1 中的封裝執行。 錯誤訊息為：「*@runincluster* 不是程序 **create_execution** 的參數。」 SSMS 的下一個版本 17.2 版中將會修正此問題。 17.2 和更新版本的 SSMS 版本在標尺出支援新的參數名稱和封裝執行。SSMS 版本 17.2 可用，以解決這個問題之前，您可以使用現有版本的 SSMS 產生封裝執行指令碼，然後變更名稱*runincluster*參數*runinscaleout*指令碼和執行指令碼中。
-   SSIS 目錄有新的全域屬性，可指定執行 SSIS 套件的預設模式。 當您呼叫此新屬性適用於**[catalog]。 [create_execution]**預存程序與*runinscaleout*參數設為 null。 此模式也適用於 SSIS SQL Agent 作業。 您可以在 SSMS 中，或使用下列命令中的 [SSISDB] 節點 [內容] 對話方塊中設定新的全域屬性：
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>在 SQL Server 2017 CTP 2.1 SSIS 的新功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在標尺出適用於 SSIS 的新增和變更功能

-   您現在可以使用**Use32BitRuntime**參數，當您使用觸發程序中向外執行。
-   已改善效能的記錄中向外的封裝執行的 SSISDB。 SSISDB 現在會寫入事件訊息和訊息內容的記錄檔而不是一個批次模式。 以下是一些關於這項改進的其他注意事項：        
    - 目前版本的 SQL Server Management Studio (SSMS) 中的某些報表目前不會執行這些記錄檔顯示在向外。我們預期情況下，它們將支援的下一個版本的 SSMS。 受影響的報表包含*所有連線*報表*錯誤內容*報表，而*連接資訊*整合服務儀表板中的區段。
    - 新的資料行**event_message_guid**已新增。 您可以使用此資料行來聯結 [catalog]。[event_message_context] 檢視和 [類別目錄]。[event_messages] 檢視，而不是使用**event_message_id**當您查詢在向外執行的這些記錄檔。
-   若要取得管理應用程式的小數位數的 SSIS 輸出[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 或更新版本。

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>SSIS SQL Server 2017 CTP 2.0 中的新功能

SQL Server 2017 CTP 2.0 中沒有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>SSIS SQL Server 2017 CTP 1.4 中的新功能

在 SQL Server 2017 CTP 1.4 中沒有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>SSIS SQL Server 2017 CTP 1.3 中的新功能

SQL Server 2017 CTP 1.3 中有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>在 SQL Server 2017 CTP 1.2 SSIS 的新功能

SQL Server 2017 CTP 1.2 中有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>SSIS SQL Server 2017 CTP 1.1 中的新功能

SQL Server 2017 CTP 1.1 中有任何新的 SSIS 功能。

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>SSIS SQL Server 2017 CTP 1.0 中的新功能

### <a name="scale-out-for-ssis"></a>SSIS 相應放大

相應放大功能讓 [!INCLUDE[ssIS_md](../includes/ssis-md.md)] 更容易在多部電腦上執行。 
   
安裝相應放大主機和背景工作之後，封裝即可發佈到不同的背景工作自動執行。 如果執行意外終止，它會自動重試。 而且，所有執行和背景工作都可以使用主機集中管理。
   
如需詳細資訊，請參閱 [Integration Services 相應放大](../integration-services/scale-out/integration-services-ssis-scale-out.md)。
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Microsoft Dynamics Online 資源的支援

OData 來源和 OData 連接管理員現在支援連接到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 摘要。


