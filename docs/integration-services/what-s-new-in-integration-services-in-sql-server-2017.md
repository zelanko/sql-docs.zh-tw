---
title: "什麼 &#39; 在 2017年的 SQL Server Integration Services 中的新 s |Microsoft 文件"
ms.custom: 
ms.date: 07/11/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 56d4ea145a34048c8619ff88112021f163e26900
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>什麼 & #39 的新 SQL Server 2017 中的 Integration Services
本主題說明 [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中已新增或更新的功能。

>   [!NOTE]
> SQL Server 2017 也包含 SQL Server 2016 的功能以及 SQL Server 2016 更新中加入的功能。 如需 SQL Server 2016 的 SSIS 新功能資訊，請參閱 [SQL Server 2016 的 Integration Services 新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)。

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>SSIS SQL Server 2017 RC1 中的新功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在標尺出適用於 SSIS 的新增和變更功能

-   相應放大主機現在支援高可用性。 您可以針對 SSISDB 啟用 Alwayson，並設定 Windows Server 容錯移轉叢集的伺服器主控標尺出主機服務。 藉由套用到標尺出 Master 的這項變更，您可以避免單一失敗點，並提供整個向外延展部署的高可用性。
-   相應放大背景工作中執行記錄的容錯移轉處理已獲得改善。 執行記錄會保存到本機磁碟，萬一標尺出背景工作意外停止。 稍後，背景工作重新啟動時，它會重新載入保存記錄檔，會繼續將它們儲存至 SSISDB。
-   為了一致性和可讀性，預存程序 **[catalog].[create_execution]** 的參數 *runincluster* 已重新命名為 *runinscaleout*。 這項變更的參數名稱具有下列影響：
    -   如果您有現有的指令碼，以向外執行封裝時，您必須變更參數名稱，從*runincluster*至*runinscaleout*以便在 RC1 中工作的指令碼。
    -   SQL Server Management Studio (SSMS) 17.1 和更早版本，所以無法觸發在 RC1 中的封裝執行。 錯誤訊息為：「*@runincluster* 不是程序 **create_execution** 的參數。」 SSMS 的下一個版本 17.2 版中將會修正此問題。 17.2 和更新版本的 SSMS 版本在標尺出支援新的參數名稱和封裝執行。 SSMS 版本 17.2 可用，以解決這個問題之前，您可以使用現有版本的 SSMS 產生封裝執行指令碼，然後變更名稱*runincluster*參數*runinscaleout*指令碼和執行指令碼中。
-   SSIS 目錄有新的全域屬性，可指定執行 SSIS 套件的預設模式。 當您呼叫此新屬性適用於**[catalog]。 [create_execution]**預存程序與*runinscaleout*參數設為 null。 此模式也適用於 SSIS SQL Agent 作業。 您可以在 SSMS 中，或使用下列命令中的 [SSISDB] 節點 [內容] 對話方塊中設定新的全域屬性：
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>在 SQL Server 2017 CTP 2.1 SSIS 的新功能

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>在標尺出適用於 SSIS 的新增和變更功能

-   您現在可以使用**Use32BitRuntime**參數，當您使用觸發程序中向外執行。
-   已改善效能的記錄中向外的封裝執行的 SSISDB。 SSISDB 現在會寫入事件訊息和訊息內容的記錄檔而不是一個批次模式。 以下是一些關於這項改進的其他注意事項：        
    - 目前版本的 SQL Server Management Studio (SSMS) 中的某些報表目前不會執行這些記錄檔顯示在向外。 我們預期情況下，它們將支援的下一個版本的 SSMS。 受影響的報表包含*所有連線*報表*錯誤內容*報表，而*連接資訊*整合服務儀表板中的區段。
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


