---
title: "加入非 SQL Server 訂閱者 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.addnonsqlsubscriber.f1"
ms.assetid: 21beeaa0-4b9e-48da-be63-1b9ff14e03d2
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# 加入非 SQL Server 訂閱者
  複寫可以支援為 Oracle 和 IBM DB2 訂閱者建立快照式和交易式發行集的發送訂閱。  
  
## 選項  
 **要加入的訂閱者類型**  
 選取 Oracle 訂閱者或 IBM DB2 訂閱者。 如需支援這些訂閱者的詳細資訊，請參閱 [非 SQL Server 訂閱者](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
 **資料來源名稱**  
 在用來尋找網路上之資料庫的名稱。 複寫會使用資料來源名稱，結合登入、密碼及您在此精靈的 **[散發代理程式安全性]** 頁面中指定的任何連接選項，來產生資料庫的連接字串。  
  
> [!NOTE]  
>  資料來源名稱和連接字串不會驗證 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 直到 「 散發代理程式會嘗試初始化訂閱。  
  
## 另請參閱  
 [Create a Subscription for a Non-SQL Server Subscriber](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [非 SQL Server 訂閱者](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  