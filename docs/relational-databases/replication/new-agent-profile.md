---
title: 新增代理程式設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 24a997bb8d14b331b8669fb2ce363b929a3279ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="new-agent-profile"></a>新增代理程式設定檔
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **[新增代理程式設定檔]** 對話方塊，即可建立新的設定檔。 新的設定檔一律會以現有設定檔為基礎，但是還可以進行修改來滿足應用程式的需求。 建立了設定檔之後，即可套用到 **[代理程式設定檔]** 對話方塊中之現有及未來的代理程式作業。 代理程式參數值可以在 [\<AgentProfileName> 屬性] 對話方塊中進行編輯。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入設定檔的名稱。  
  
 **說明**  
 輸入設定檔的描述。  
  
 **參數**  
 設定檔中包括的代理程式參數。 作為新設定檔之基礎的設定檔，並不一定會為每一個參數都指定值。 若要檢視給定代理程式的所有有效參數，請清除 **[只顯示這個設定檔中使用的參數]** 核取方塊。 如需每一個參數的描述，請參閱：  
  
-   [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [複寫佇列讀取器代理程式](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **預設值**  
 每一個代理程式參數的預設值。  
  
 **值**  
 針對作為新設定檔之基礎的設定檔中，所指定的參數值。 編輯此欄位，即可變更參數的值。  
  
 **[只顯示這個設定檔中使用的參數]**  
 清除即可顯示給定代理程式的所有有效參數。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
