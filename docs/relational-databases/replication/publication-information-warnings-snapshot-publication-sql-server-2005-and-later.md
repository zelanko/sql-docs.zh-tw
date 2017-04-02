---
title: "發行集資訊，警告 (快照式發行集，SQL Server 2005 和更新的版本) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publicationinfo.warningsandagents.snapshot.f1"
ms.assetid: 7aa2eb52-b6b7-4dd3-8483-8ef00d9f0435
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 發行集資訊，警告 (快照式發行集，SQL Server 2005 和更新的版本)
  執行 **和更新版本的散發者可以使用** [警告] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 索引標籤。 **[警告]** 索引標籤可以讓您針對選取的發行集執行下列工作：  
  
-   啟用警告。  
  
-   指定與警告相關聯的臨界值。  
  
-   定義與警告相關聯的警示。  
  
## 警告、臨界值和警示  
 根據預設，複寫監視器會針對未初始化的訂閱顯示警告： **[未初始化的訂閱]** 狀態會在包含訂閱資訊之頁面的 **[狀態]** 資料行中顯示為警告。 快照式發行集，您也可以指定即將發生訂閱逾期時會產生警告選項 **若訂閱將在臨界值內過期，即發出警告**。 如果達到或超過指定的臨界值，訂閱狀態會顯示為 **即將過期/已過期** （除非需要顯示優先順序較高的問題）。  
  
 除了在複寫監視器顯示警告外，達到臨界值也會觸發警示。 定義警示的方式，是按一下 **[設定警示]** ，並在 **[設定複寫警示]** 對話方塊中提供資訊。  
  
## 選項  
 **已啟用**  
 選取以啟用警告，並指定臨界值。  
  
 **警告**  
 與臨界值相關聯之警告的描述。  
  
 **臨界值**  
 指定臨界值的值。  
  
 **設定警示**  
 選取的資料列中 **警告** 方格中，然後按一下 [ **設定警示** 啟動 **設定複寫警示** 對話方塊。 此對話方塊可以讓您定義與選取的臨界值和警告相關聯的警示。  
  
 **捨棄變更**  
 按一下即可捨棄對警告與臨界值所做的任何變更。  
  
> [!NOTE]  
>  按一下 **放棄變更** 中定義的警示並不會影響 **設定複寫警示** 對話方塊。  
  
 **儲存變更**  
 按一下即可儲存對警告與臨界值所做的任何變更。  
  
## 另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視資訊並執行工作的發行集與 #40。複寫監視器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  