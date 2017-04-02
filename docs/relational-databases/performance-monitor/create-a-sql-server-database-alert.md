---
title: "建立 SQL Server 資料庫警示 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料庫效能 [SQL Server]，警示"
  - "警示 [SQL Server], 建立"
  - "臨界值 [SQL Server]"
  - "資料庫警示 [SQL Server]"
  - "微調資料庫 [SQL Server]，警示"
  - "監視效能 [SQL Server]，警示"
  - "監視伺服器效能 [SQL Server]，警示"
  - "資料庫監視 [SQL Server]，警示"
  - "伺服器效能 [SQL Server]，警示"
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# 建立 SQL Server 資料庫警示
  您可以使用「系統監視器」來建立警示，讓它在達到「系統監視器」計數器的臨界值時引發。 為了回應此警示，「系統監視器」可啟動某個應用程式，諸如撰寫來處理此警示條件的自訂應用程式。 例如，您可以建立一個警示，讓它在死結 (Deadlock) 個數超過特定數值時引發。  
  
 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來定義警示。 如需詳細資訊，請參閱 [警示](../../ssms/agent/alerts.md)。  
  
 如需使用「系統監視器」來建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫警示的詳細資訊，請參閱[設定 SQL Server 資料庫警示 &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)。  
  
## 另請參閱  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  