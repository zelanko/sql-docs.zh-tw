---
title: "新增代理程式設定檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.profiles.newperfprofile.f1"
helpviewer_keywords: 
  - "新增代理程式設定檔對話方塊"
ms.assetid: ebf59330-a421-45a5-9020-0484a96852bc
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 新增代理程式設定檔
  使用 **新代理程式設定檔** 對話方塊來建立新的設定檔。 新的設定檔一律會以現有設定檔為基礎，但是還可以進行修改來滿足應用程式的需求。 在建立設定檔之後，它可以套用至現有和未來的代理程式作業中 **代理程式設定檔** 對話方塊。 代理程式參數值可以在編輯 \<**AgentProfileName > 屬性** 對話方塊。  
  
## 選項  
 **名稱**  
 輸入設定檔的名稱。  
  
 **描述**  
 輸入設定檔的描述。  
  
 **參數**  
 設定檔中包括的代理程式參數。 作為新設定檔之基礎的設定檔，並不一定會為每一個參數都指定值。 若要檢視給定代理程式的所有有效參數，請清除 **[只顯示這個設定檔中使用的參數]** 核取方塊。 如需每一個參數的描述，請參閱：  
  
-   [複寫快照集代理程式](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
-   [複寫記錄讀取器代理程式](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
-   [複寫散發代理程式](../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
-   [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)  
  
-   [複寫佇列讀取器代理程式](../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
 **預設值**  
 每一個代理程式參數的預設值。  
  
 **值**  
 針對作為新設定檔之基礎的設定檔中，所指定的參數值。 編輯此欄位，即可變更參數的值。  
  
 **只顯示這個設定檔中使用的參數。**  
 清除即可顯示給定代理程式的所有有效參數。  
  
## 另請參閱  
 [Work with Replication Agent Profiles](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  