---
title: "How to Manage a CDC Instance |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d368fcacfb8e548647785c8b5f6ef5b73b4ef10b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-manage-a-cdc-instance"></a>如何管理 CDC 執行個體
  此程序描述如何使用 CDC 設計工具主控台，於執行階段管理 CDC 執行個體操作。  
  
### <a name="to-manage-cdc-instance-operations"></a>若要管理 CDC 執行個體操作  
  
1.  從 **[開始]** 功能表選取 **[CDC 設計工具主控台]**。  
  
2.  在左窗格中展開 **[異動資料擷取]** ，然後展開包含您要檢視之執行個體的服務。  
  
3.  選取您要使用的執行個體名稱。  
  
4.  從 CDC 設計工具主控台右側的 **[動作]** 窗格中，按一下您想要執行的操作。  
  
     您也可以在左窗格中，以滑鼠右鍵按一下執行個體的名稱，並選取您想要執行的操作。  
  
     您可以執行以下工作：  
  
    -   **啟動**：開始擷取變更。  
  
    -   **停止**：停止擷取變更。  
  
    -   **重設**：按一下 [重設]，將 CDC 執行個體重設為初始 (空白) 狀態。 當 CDC 執行個體停止時可以使用這個選項。 變更資料表及 CDC 執行個體內部狀態的所有變更都會遭到刪除。 之後啟動 CDC 執行個體時，異動擷取將會從該時間點開始，而且只包含 CDC 執行個體啟動之後所開始的交易。  
  
    -   **刪除**：刪除 CDC 執行個體。  
  
    -   **Oracle 記錄指令碼**： 按一下**Oracle 記錄指令碼**顯示 Oracle 補充記錄指令碼與 Oracle 記錄指令碼對話方塊方塊。 如需有關您可以在此對話方塊中執行之操作的詳細資訊，請參閱＜ [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md)＞。  
  
         **注意**：當您執行補充記錄指令碼時，將會開啟 [執行指令碼的 Oracle 認證] 對話方塊，您可以在此提供有效的 Oracle 使用者名稱和密碼。 如需有關如何提供適當之 Oracle 認證的詳細資訊，請參閱＜ [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)＞。  
  
    -   **CDC 執行個體部署**：產生 CDC 執行個體的部署指令碼。 如需有關此對話方塊的詳細資訊，請參閱＜ [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md)＞。  
  
     如需有關這些工作的詳細資訊，請參閱＜ [Manage a CDC Instance](../../integration-services/change-data-capture/manage-a-cdc-instance.md)＞。  
  
 您也可以選取 **[屬性]** 來編輯 CDC 執行個體組態屬性。 如需有關編輯 CDC 執行個體屬性的詳細資訊，請參閱＜ [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md)＞。  
  
  
