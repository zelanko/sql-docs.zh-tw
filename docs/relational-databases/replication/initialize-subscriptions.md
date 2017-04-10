---
title: "初始化訂閱 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 初始化訂閱
  訂閱者必須先初始化，才能開始接收複寫的資料。 不需要有初始資料集，但訂閱者至少必須有每個複寫物件的結構描述，以及複寫所需的任何中繼資料表和程序。  
  
## 選項  
 **訂閱屬性**  
 選取核取方塊，在 **初始化** 需要初始資料集的每一個訂閱者的資料行。 如果清除此核取方塊，則只會初始化複寫中繼資料和程序。 如需初始化訂閱不使用快照集的詳細資訊，請參閱 [初始化交易式訂閱不使用快照集](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
 選取 **立即** 從下拉式清單方塊中 **初始化時機** 資料行具有 「 合併代理程式 」 或 「 散發代理程式傳送快照集檔案至 「 訂閱者 」 完成此精靈。 選取 **[第一次同步處理時]** ，即可使代理程式在下一個執行排程傳送檔案。  **立即** 選項不適用於提取訂閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。 合併代理程式或散發代理程式無法在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的執行個體上執行；因此必須經由其他方法初始化訂閱。  
  
> [!NOTE]  
>  精靈可能會提示散發者的連接，以便為散發者代理程式或合併代理程式啟動適當的作業。  
  
## 另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  