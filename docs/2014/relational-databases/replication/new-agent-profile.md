---
title: 新增代理程式設定檔 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.profiles.newperfprofile.f1
helpviewer_keywords:
- New Agent Profile dialog box
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f817afb2364728b93718f9dc5831b501f681d9f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070608"
---
# <a name="new-agent-profile"></a>新增代理程式設定檔
  使用 **[新增代理程式設定檔]** 對話方塊，即可建立新的設定檔。 新的設定檔一律會以現有設定檔為基礎，但是還可以進行修改來滿足應用程式的需求。 建立了設定檔之後，即可套用到 **[代理程式設定檔]** 對話方塊中之現有及未來的代理程式作業。 代理程式參數值可以在 [\<AgentProfileName> 屬性] 對話方塊中進行編輯。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入設定檔的名稱。  
  
 **說明**  
 輸入設定檔的描述。  
  
 **參數**  
 設定檔中包括的代理程式參數。 作為新設定檔之基礎的設定檔，並不一定會為每一個參數都指定值。 若要檢視給定代理程式的所有有效參數，請清除 **[只顯示這個設定檔中使用的參數]** 核取方塊。 如需每一個參數的描述，請參閱：  
  
-   [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
-   [複寫記錄讀取器代理程式](agents/replication-log-reader-agent.md)  
  
-   [Replication Distribution Agent](agents/replication-distribution-agent.md)  
  
-   [複寫合併代理程式](agents/replication-merge-agent.md)  
  
-   [複寫佇列讀取器代理程式](agents/replication-queue-reader-agent.md)  
  
 **預設值**  
 每一個代理程式參數的預設值。  
  
 **值**  
 針對作為新設定檔之基礎的設定檔中，所指定的參數值。 編輯此欄位，即可變更參數的值。  
  
 **[只顯示這個設定檔中使用的參數]**  
 清除即可顯示給定代理程式的所有有效參數。  
  
## <a name="see-also"></a>另請參閱  
 [處理複寫代理程式設定檔](agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式概觀](agents/replication-agents-overview.md)   
 [複寫代理程式設定檔](agents/replication-agent-profiles.md)  
  
  
