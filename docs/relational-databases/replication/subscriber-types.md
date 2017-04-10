---
title: "訂閱者類型 | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.subscribertypes.f1"
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 訂閱者類型
  合併式複寫可讓您指定發行集必須支援的訂閱者類型。 選取訂閱者類型會設定 *發行集相容性層級*，以決定發行集可以使用哪些功能。  
  
 建立發行集快照集之後，可以 （設定更多限制） 增加發行集相容性層級上 **一般** 頁面 **發行集屬性** ] 對話方塊中，相容性層級不能減少。  
  
## 選項  
 選取此發行集必須支援的每個訂閱者類型。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 發行集可以使用所有的功能。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 發行集需要快照集檔案為字元格式 (這可由快照集代理程式自動處理)。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 也有許多與相容性層級無關的限制。  
  
 如果選取此選項，就會啟用發行集的 Web 同步處理選項。 如需有關 Web 同步處理的詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
## 另請參閱  
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [屬性參考 & #40。複寫 & #41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  