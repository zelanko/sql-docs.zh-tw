---
title: "發行者 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configuredistributionwizard.enablepublishers.f1"
ms.assetid: 116cd6a5-32ac-4273-81a2-d184408e0f07
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 發行者
  您可以提供權限讓其他發行者使用此散發者。 請注意，讓發行者可以使用這個伺服器作為它的遠端散發者，並不會使該伺服器成為發行者。 您必須連接到發行者，設定其發行，並選擇此伺服器為散發者。 您可以透過新增發行集精靈來設定發行者和選擇散發者。  
  
 您選取作為發行者的伺服器，將使用此精靈的 **[散發資料庫]** 頁面上指定的散發資料庫。 如果您要使用不同的散發資料庫，此時請不要啟用發行者。 在完成設定散發精靈之後，請改用 **[散發者屬性]** 對話方塊來加入發行者。  
  
## 選項  
 **發行者**  
 選取可使用這個散發者的伺服器。 按一下屬性按鈕 (**...**) 來檢視和設定其他屬性的 「 發行者 」 旁邊。  
  
 **加入**  
 如果沒有列出您想要允許的伺服器，按一下 [ **新增** 新增 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者或 Oracle 發行者加入可用發行者的清單。  
  
## 另請參閱  
 [設定散發](../../relational-databases/replication/configure-distribution.md)   
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
  