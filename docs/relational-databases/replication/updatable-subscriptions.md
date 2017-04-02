---
title: "可更新的訂閱 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.updatablesubscriptions.f1"
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 可更新的訂閱
  異動複寫，複寫的資料應視為為唯讀。不過，您可以修改複寫的資料 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者端使用可更新訂閱。 如果您需要修改訂閱者端的資料，請視您的需求，使用下列其中一個選項。  
  
|可更新的訂閱類型|需求|  
|---------------------------------|------------------|  
|立即更新|發行者及訂閱者必須已建立連接，才能更新訂閱者端的資料。|  
|佇列更新|發行者和訂閱者不需要連接，即可更新訂閱者端的資料。 可以在離線時進行更新，並於稍後在發行者和訂閱者之間進行同步處理。|  
  
## 選項  
 **複寫訂閱者變更**  
 選取核取方塊，在 **複寫** 針對每個訂閱者，應該能夠進行更新的資料行。 訂閱者，可以進行更新，從下拉式清單方塊中選取適當的選項 **在發行者端認可** 資料行︰  
  
-   選取 **同時認可變更** 針對立即更新訂閱。  
  
-   選取 **佇列變更且儘可能認可** 針對佇列更新訂閱。  
  
## 另請參閱  
 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  