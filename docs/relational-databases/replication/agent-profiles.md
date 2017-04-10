---
title: "代理程式設定檔 | Microsoft Docs"
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
  - "sql13.rep.profiles.perfprofiles.f1"
helpviewer_keywords: 
  - "代理程式設定檔對話方塊"
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 代理程式設定檔
  使用 **[代理程式設定檔]** 對話方塊，即可管理代理程式設定檔。 代理程式設定檔提供便於管理每一個代理程式執行階段參數的方式。 每一個代理程式都有預設的設定檔，有些代理程式還有其他預先定義的設定檔。 例如，合併代理程式有專為低頻寬連接設計的「慢速連結」設定檔。 預先定義的設定檔對大部份應用程式而言已經足夠，但您也可以建立使用者自訂設定檔，來自訂代理程式的行為。  
  
## 選項  
 **選取頁面**  
 在左窗格中選取代理程式，右窗格就會顯示代理程式的設定檔。  
  
 **新項目的預設值**  
 選取為指定類型之代理程式建立作業時所使用的設定檔。 例如，若您對合併式發行集建立一些訂閱，則每一個訂閱的合併代理程式作業就會使用所選取的設定檔。 如果您要變更現有作業的設定檔，請選取設定檔，然後按一下 **[變更現有的代理程式]**。  
  
 **名稱**  
 設定檔的名稱。  
  
 **型別**  
 設定檔的類型︰ **使用者** （使用者定義） 或 **系統** （預先定義的）。  
  
 **屬性 (...)**  
 按一下即可檢視代理程式設定檔中，每一個參數所使用的值。  
  
 **新增**  
 按一下即可建立新的設定檔。  
  
 **Delete**  
 選取的使用者定義設定檔，然後按一下 **刪除** 刪除該設定檔。 預先定義的設定檔無法刪除。  
  
 **變更現有的代理程式**  
 選取設定檔，然後再按 **變更現有的代理程式** 來指定特定類型的代理程式的所有現有的作業應該使用選取的設定檔。 例如，若您對合併式發行集建立了一些訂閱，但您要變更設定檔，以指定每個訂閱的合併代理程式作業都使用 **[慢速連結代理程式設定檔]**，請選取該設定檔，然後按一下 **[變更現有的代理程式]**。  
  
## 另請參閱  
 [Work with Replication Agent Profiles](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫代理程式設定檔](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  