---
title: "使用系統監視器監視複寫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "監視效能 [SQL Server 複寫], 系統監視器"
  - "系統監視器 [SQL Server], 複寫"
  - "效能計數器 [SQL Server 複寫]"
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 使用系統監視器監視複寫
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 系統監視器可讓您使用圖形、 圖表和報告來量測電腦的效率並識別和排除可能的問題 （例如不平衡的資源使用量、 硬體不足或不良的程式設計），並規劃其他硬體需求。 如需詳細資訊，請參閱 [監視資源使用量 & #40。系統監視器 & #41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)。  
  
 「系統監視器」使用效能物件和計數器，這些工具可以提供各種處理之效能的資訊。 您可以透過與複寫代理程式相關的計數器來衡量複寫效能：  
  
|代理程式|效能物件|計數器|描述|  
|-----------|------------------------|-------------|-----------------|  
|所有代理程式|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：複寫代理程式|執行中|目前正在執行的複寫代理程式數。|  
|快照集代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫快照集|Snapshot:Delivered Cmds/sec|每秒傳送到散發者的命令數。|  
|快照集代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫快照集|Snapshot:Delivered Trans/sec|每秒傳送到散發者的交易數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫記錄讀取器|Logreader:Delivered Cmds/sec|每秒傳送到散發者的命令數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫記錄讀取器|Logreader:Delivered Trans/sec|每秒傳送到散發者的交易數。|  
|記錄讀取器代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫記錄讀取器|Logreader:Delivery Latency|「發行者」套用交易時，該交易傳送至「散發者」所花費的時間，以毫秒為單位。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication dist.|Dist:Delivered Cmds/sec|每秒傳遞至「訂閱者」的命令數。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication dist.|Dist:Delivered Trans/sec|每秒傳遞至「訂閱者」的交易數。|  
|散發代理程式|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Replication dist.|Dist:Delivery Latency|目前從交易傳送到分配者到交易在「訂閱者」套用所經過的時間 (毫秒)。|  
|[合併代理程式]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫合併|Conflicts/sec|合併處理期間每秒所發生的衝突數。|  
|[合併代理程式]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫合併|Downloaded Changes/sec|每秒從「發行者」複寫至「訂閱者」的資料列數。|  
|[合併代理程式]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]︰ 複寫合併|Uploaded Changes/sec|每秒從「訂閱者」複寫至「發行者」的資料列數。|  
  
## 另請參閱  
 [監視和 #40。複寫 & #41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  