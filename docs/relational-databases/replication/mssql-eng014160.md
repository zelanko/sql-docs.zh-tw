---
title: "MSSQL_ENG014160 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014160 錯誤"
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014160
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14160|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|已設定臨界值 [%s:%s] (針對發行集 [%s])。 此發行集的一個或多個訂閱已經到期。|  
  
## 說明  
 複寫可讓您啟用多個條件的警告。 這包括訂閱即將過期。 如果未同步處理使訂閱過期內指定 *保留期限*。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 當您啟用警告使用複寫監視器或 [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md), ，指定可決定何時觸發警告臨界值。 當達到或超過臨界值時，複寫監視器中會顯示警告，而且會有事件寫入 Windows 事件記錄檔。 達到臨界值也會觸發 SQL Server Agent 警示。 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) 和 [以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)。  
  
## 使用者動作  
 此問題的解決方案需視引發警告的原因而定：  
  
-   如果已超過臨界值，但是訂閱尚未過期，請同步處理訂閱。 如需詳細資訊，請參閱 [同步處理資料](../../relational-databases/replication/synchronize-data.md)。  
  
-   如果代理程式已經在執行，但未正確複寫變更，可能會導致訂閱過期。 進行異動複寫時，請確認散發代理程式和記錄讀取器代理程式正在執行。 進行合併式複寫時，請確認合併代理程式正在執行。 如何啟動這些代理程式的相關資訊，請參閱 [啟動和停止複寫代理程式 & #40。SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和 [複寫代理程式可執行檔概念](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)。  
  
-   如果訂閱已過期，則必須重新初始化，或是卸除後再重新建立，需視訂閱類型及已過期時間的長短而定。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  