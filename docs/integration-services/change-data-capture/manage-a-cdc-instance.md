---
title: "管理 CDC 執行個體 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b61e0362a4b29f1721a08469f8df529861e10174
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="manage-a-cdc-instance"></a>管理 CDC 執行個體
  您可以使用 CDC 設計工具主控台來檢視有關您所建立之執行個體的資訊，並管理執行個體的操作。  
  
 在左窗格中按一下執行個體的名稱，以檢視有關此執行個體的資訊。  
  
> [!NOTE]  
>  如果您在左窗格中選取服務，可用執行個體的清單也會顯示在 CDC 設計工具主控台的中央。 如果您在此區段中選取其中一個執行個體，您可以在右窗格執行工作；但是，您將無法檢視屬性索引標籤中的資訊。  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>您在顯示 CDC 執行個體資訊時可以做什麼事  
 從右窗格執行以下動作：  
  
 **啟動**  
 按一下 [啟動]，開始擷取選定 CDC 執行個體的變更。  
  
 **停止**  
 按一下 [停止]，停止擷取選定 CDC 執行個體的變更。 當您停止 CDC 執行個體時，擷取至該點的變更不會遺失，而且在 CDC 執行個體恢復時會傳遞這些變更。  
  
 **重設**  
 按一下 [重設]，將 CDC 執行個體重設為初始 (空白) 狀態。 當 CDC 執行個體停止時可以使用這個選項。 變更資料表及 CDC 執行個體內部狀態的所有變更都會遭到刪除。 之後啟動 CDC 執行個體時，異動擷取將會從該時間點開始，而且只包含 CDC 執行個體啟動之後所開始的交易。  
  
 在確認對話方塊中按一下 **[確定]** ，確認您想要重設 CDC 執行個體，並刪除寫入變更資料表的變更。  
  
 **刪除**  
 按一下 [刪除]，永久刪除 CDC 執行個體。 只有當 CDC 執行個體停止時才可以使用這個選項。  
  
 在確認對話方塊中按一下 **[確定]** ，確認您想要刪除 CDC 執行個體。  
  
 **Oracle 記錄指令碼**  
 按一下這個連結可顯示 [Oracle 記錄指令碼] 對話方塊，其中包含 Oracle 補充記錄指令碼。 如需有關您可以在此對話方塊中執行之操作的詳細資訊，請參閱＜ [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md)＞。  
  
> [!NOTE]  
>  當您執行補充記錄指令碼時，將會開啟 [執行指令碼的 Oracle 認證] 對話方塊，您可以在此提供有效的 Oracle 使用者名稱和密碼。 如需有關如何提供適當之 Oracle 認證的詳細資訊，請參閱＜ [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)＞。  
  
 **CDC 執行個體部署指令碼**  
 按一下這個連結可顯示 [CDC 執行個體部署指令碼] 對話方塊，此對話方塊會顯示 CDC 執行個體部署指令碼。 如需有關此對話方塊的詳細資訊，請參閱＜ [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md)＞。  
  
 **屬性**  
 按一下此連結即可開啟屬性編輯器。 您可使用屬性編輯器來編輯 CDC 執行個體組態。 如需有關編輯 CDC 執行個體之屬性的詳細資訊，請參閱＜ [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md)＞。  
  
 **檢視器索引標籤**  
  
 當您檢視 CDC 執行個體的資訊時，可使用以下的檢視器索引標籤。 這些索引標籤中的資訊是唯讀的。  
  
 **狀態**  
 此索引標籤會提供有關 CDC 執行個體目前狀態的資訊和統計資料。 其中包含以下資訊。  
  
-   **狀態**：指示 CDC 執行個體之目前狀態的圖示。 下面會描述這些狀態。  
  
    |||  
    |-|-|  
    |![錯誤](../../integration-services/change-data-capture/media/error.gif "錯誤")|**錯誤**： Oracle CDC 執行個體未在執行中，因為發生無法重試的錯誤。 以下是可用的子狀態：<br /><br /> **設定錯誤**：發生了需要手動介入的組態錯誤。<br /><br /> **需要密碼**：未針對 Oracle CDC 執行個體設定任何密碼，或是密碼無效。<br /><br /> **非預期**： 所有其他無法復原的錯誤。|  
    |![確定](../../integration-services/change-data-capture/media/okay.gif "確定")|**執行中**：CDC 執行個體正在執行及處理變更記錄。 以下是可用的子狀態：<br /><br /> **閒置**：所有變更記錄都已經處理並儲存在目標變更資料表中。 沒有其他使用中交易。<br /><br /> **正在處理**：有正在處理但是尚未寫入變更資料表的變更記錄。|  
    |![停止](../../integration-services/change-data-capture/media/stop.gif "停止")|**已停止**：CDC 執行個體未在執行中。 已停止的狀態表示 CDC 執行個體以正常方式停止。|  
    |![已暫停](../../integration-services/change-data-capture/media/paused.gif "已暫停")|**已暫停**：CDC 執行個體正在執行中，但是因為發生可重試的錯誤所以暫停處理。 以下是可用的子狀態：<br /><br /> **已中斷連接**：無法建立與來源 Oracle 資料庫的連接。 還原連接時，處理作業便會繼續。<br /><br /> **儲存體**：儲存體已滿。 當有額外的儲存體可用時，處理作業便會繼續。<br /><br /> **記錄器**：記錄器連接到 Oracle，但由於暫時性問題無法讀取 Oracle 交易記錄，例如，無法使用必要的交易記錄。|  
  
-   **詳細狀態**：目前的子狀態。  
  
-   **狀態訊息**：有關目前狀態的詳細資訊。  
  
-   **時間戳記**：上次從狀態資料表讀取 CDC 狀態時的 UTC 時間。  
  
-   **目前正在處理**：您會在此區段中監視以下資訊。  
  
    -   **上次交易時間戳記**：上次交易寫入變更資料表時的當地時間。  
  
    -   **上次變更時間戳記**：來源 Oracle 資料庫交易記錄中的 Oracle CDC 執行個體查看最近變更時的當地時間。 這會提供有關 CDC 執行個體讀取 Oracle 交易記錄之目前延遲的資訊。  
  
    -   **交易記錄標頭 CN**：從 Oracle 交易記錄讀取的最近變更編號 (CN)。  
  
    -   **交易記錄結尾 CN**：復原或重新啟動 CDC 執行個體的變更編號。 萬一重新啟動或發生任何其他類型的失敗 (包括叢集容錯移轉)，Oracle CDC 執行個體將會重新調整到這個位置。  
  
    -   **目前 CN**：來源 Oracle 資料庫 (不是交易記錄) 中看到的上次變更編號 (SCN)。  
  
    -   **使用中交易**：Oracle CDC 執行個體正在處理而且尚未決定 (認可/回復) 之來源 Oracle 交易的目前數目。  
  
    -   **暫存交易**：暫存至 [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) 資料表之來源 Oracle 交易的目前數目。  
  
-   **計數器**：您會在此區段中監視以下資訊。  
  
    -   **完成的交易**：上次重設 CDC 執行個體之後完成的交易數目。 這不包括未包含相關資料表的交易。  
  
    -   **寫入的變更**：寫入 SQL Server 變更資料表的變更數目。  
  
 **Oracle**  
 顯示有關 CDC 執行個體以及它與 Oracle 資料庫之連接的資訊。 此索引標籤是唯讀的。 若要編輯這些屬性，請以滑鼠右鍵在左窗格中按一下執行個體，並選取 [屬性] 或按一下右窗格中的 [屬性]，開啟 [\<執行個體> 屬性] 對話方塊。  
  
 如需有關這些屬性以及如何加以編輯的詳細資訊，請參閱＜ [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md)＞。  
  
 **資料表**  
 顯示有關 CDC 執行個體中包含之資料表的資訊。 這裡也會提供資料行資訊。 此索引標籤是唯讀的。 若要編輯這些屬性，請以滑鼠右鍵在左窗格中按一下執行個體，並選取 [屬性] 或按一下右窗格中的 [屬性]，開啟 [\<執行個體> 屬性] 對話方塊。  
  
 如需有關這些屬性以及如何加以編輯的詳細資訊，請參閱＜ [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)＞。  
  
 **進階**  
 顯示 CDC 執行個體的進階屬性和屬性值。 此索引標籤是唯讀的。 若要編輯這些屬性，請以滑鼠右鍵在左窗格中按一下執行個體，並選取 [屬性] 或按一下右窗格中的 [屬性]，開啟 [\<執行個體> 屬性] 對話方塊。  
  
 如需有關這些屬性以及如何加以編輯的詳細資訊，請參閱＜ [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [如何檢視 CDC 執行個體屬性](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [如何編輯 CDC 執行個體屬性](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [使用 [新增執行個體精靈]](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
