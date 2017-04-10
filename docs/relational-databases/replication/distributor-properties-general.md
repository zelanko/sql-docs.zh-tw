---
title: "散發者屬性，一般 | Microsoft Docs"
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
  - "sql13.rep.configdistwizard.distproperties.general.f1"
helpviewer_keywords: 
  - "散發者屬性對話方塊"
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 散發者屬性，一般
  **[散發者屬性]** 對話方塊的 **[一般]** 頁面可讓您加入和刪除散發資料庫，以及設定散發資料庫屬性。  
  
 散發資料庫會儲存所有複寫類型的中繼資料和記錄資料，以及異動複寫的交易。 在許多情況下，單一散發資料庫即已足夠。 但是如果多個發行者使用單一散發者，請考慮為每個發行者建立散發資料庫。 這樣可以確保流經每個散發資料庫的資料都不同。  
  
## 選項  
 **資料庫**  
  **資料庫** 屬性方格會顯示 「 散發者 」 之散發資料庫的名稱與保留屬性。 **交易保留** 是交易式複寫儲存交易的時間長度 （交易保留又稱為散發保留）。 **[記錄保留]** 是為所有的複寫類型儲存記錄中繼資料的時間長度。 如需有關散發保留的詳細資訊，請參閱 [訂閱逾期與停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 按一下屬性按鈕 (**...**) 中 **資料庫** 屬性方格] 來啟動 **散發資料庫屬性** 對話方塊。  
  
 **新增**  
 按一下即可建立新的散發資料庫。  
  
 **Delete**  
 選取現有的散發資料庫中 **資料庫** 屬性方格中，然後按一下 [ **刪除** 刪除資料庫。 如果只有一個這種資料庫，就無法刪除此散發資料庫；每個散發者至少必須有一個散發資料庫。 若要刪除所有的散發資料庫，您必須停用電腦上的散發。 如需詳細資訊，請參閱 [停用發行與散發](../../relational-databases/replication/disable-publishing-and-distribution.md)。  
  
 **設定檔預設值**  
 按一下以存取複寫代理程式設定檔中 **代理程式設定檔** 對話方塊。 如需有關設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)＞。  
  
## 另請參閱  
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  