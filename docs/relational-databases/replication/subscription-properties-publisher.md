---
title: "訂閱屬性 - 發行者 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.subproperties.publisher.f1"
helpviewer_keywords: 
  - "訂閱屬性對話方塊"
ms.assetid: d4b2bc8b-0431-4331-8305-8992c96d0d34
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 訂閱屬性 - 發行者
   **訂閱屬性** 對話方塊在 「 發行者 」 可讓您檢視和設定發送訂閱的屬性。 您也可以檢視提取訂閱的某些屬性，但 **訂閱屬性** 「 訂閱者 」 的對話方塊中顯示其他屬性，並允許修改屬性。  
  
 在每個屬性 **訂閱屬性** ] 對話方塊中包含的描述。 按一下某個屬性，即可查看其在對話方塊底部顯示的描述。 此主題提供了關於一些屬性的其他資訊，其中大多數屬性僅會針對發行者端的發送訂閱顯示。 屬性會依下列類別目錄分組：  
  
-   套用至所有訂閱的屬性。  
  
-   套用至交易式訂閱的屬性。  
  
-   套用至合併訂閱的屬性。  
  
 如果選項顯示為唯讀，則只有在建立訂閱時才能設定。 如果想要設定新增訂閱精靈中無法使用的選項，請以預存程序建立訂閱。 如需相關資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 及 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
## 所有訂閱的選項。  
 **安全性**  
 按一下 [ **代理程式處理帳戶** 資料列，然後按一下 [內容] 按鈕 (**...**) 若要變更散發代理程式 」 或 「 合併代理程式在散發者上執行的帳戶。 若要變更的散發代理程式 」 或 「 合併代理程式會連接到 「 訂閱者 」 的帳戶，請按一下 [ **訂閱者連接**, ，然後按一下屬性按鈕 (**...**)。  
  
 如需每個代理程式所需的權限的詳細資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
## 交易式訂閱的選項  
 **防止交易迴圈**  
 決定散發代理程式是否要將源自訂閱者端的交易，傳送回到訂閱者端。 此選項適用於雙向異動複寫。 如需詳細資訊，請參閱 [雙向異動複寫](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)。  
  
 **可更新的訂閱**  
 決定訂閱者變更是否會複寫回發行者。 可以使用佇列更新或立即更新來複寫變更。 選擇 **訂閱者更新方法** 決定要使用的方法。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
## 合併訂閱的選項  
 **資料分割定義 (HOST_NAME)**  
 合併式複寫的發行集使用參數化篩選，以判斷應該會收到 「 訂閱者 」 的資料同步處理期間評估兩個系統函數 （或兩者如果篩選參考兩個函式） 的其中一個︰ **suser_sname （)** 或 **host_name （)**。 根據預設， **host_name （)** 傳回的電腦上的 「 合併代理程式正在執行，但是您可以覆寫此值新增訂閱精靈 」 中的名稱。 如需有關參數化的篩選，覆寫 **host_name （)**, ，請參閱 [參數化資料列篩選](../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
 **訂閱類型** 和 **優先順序**  
 顯示訂閱是客訂閱或主訂閱 (建立了訂閱之後就無法再變更)。 主訂閱可以將資料重新發行至其他訂閱者，並且可以指派衝突解決的優先權。  
  
 如果您在新增訂閱精靈中選取伺服器的訂閱類型，就會為訂閱者指定在衝突解決過程中使用的優先權。  
  
 **以互動方式解決衝突**  
 決定在合併同步處理過程中，是否使用互動解析程式使用者介面來解決衝突。 這需要的值為 **啟用** 的 **使用 Windows Synchronization Manager**。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](../../relational-databases/replication/merge/interactive-conflict-resolution.md)。  
  
## 另請參閱  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  