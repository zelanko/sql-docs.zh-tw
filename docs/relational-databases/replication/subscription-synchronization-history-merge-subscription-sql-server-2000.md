---
title: "訂閱，同步處理記錄 (合併訂閱，SQL Server 2000) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.subscription.downlevelsynchhistory.f1"
ms.assetid: 0a0deab2-1c08-4371-9681-d9403e0236cc
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# 訂閱，同步處理記錄 (合併訂閱，SQL Server 2000)
  **[同步處理記錄]** 索引標籤會顯示有關合併代理程式的詳細資訊，包括狀態、記錄、參考訊息及任何錯誤訊息。  
  
## 選項  
 從 [檢視]  功能表中選取要檢視的合併代理程式工作階段，再於 [合併代理程式工作階段] 方格中選取特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]**之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **檢視**  
 選取要檢視的合併代理程式工作階段。 合併代理程式通常會連續執行，因此可能只會有一個工作階段可供檢視。  
  
 **狀態**  
 合併代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   已完成  
  
-   正在重試  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 合併代理程式在這個工作階段中執行的時間量。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段結束時發生錯誤，這個欄位會顯示合併代理程式記錄的最後一個錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 合併代理程式在選取的工作階段期間已記錄的所有參考訊息和錯誤訊息。  
  
 **動作時間**  
 動作中描述的時間 **動作訊息** 執行資料行。  
  
 **所選取之工作階段的錯誤詳細資料或訊息**  
 顯示所選工作階段顯示的值時，才 **錯誤** 中 **狀態** 資料行。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## 另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視資訊並執行訂閱 & #40; 相關聯的代理程式工作複寫監視器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  