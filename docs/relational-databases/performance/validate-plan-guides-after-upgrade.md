---
title: "升級之後驗證計畫指南 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-plan-guides"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "計劃指南 [SQL Server], 升級之後驗證"
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 升級之後驗證計畫指南
  建議您將應用程式升級為新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，重新評估和測試計畫指南定義。 效能微調需求和計畫指南符合的行為有可能會變更。 雖然無效的計畫指南不會導致查詢失敗，但是系統將不會使用此計畫指南來編譯計畫，而且此計畫可能不是最佳選擇。 將資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，我們建議您執行下列工作：  
  
-   使用 [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) 函數來驗證現有的計畫指南。  
  
-   使用擴充事件，透過 [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) 事件，在一段時間內監視是否有誤導的計畫。  
  
  