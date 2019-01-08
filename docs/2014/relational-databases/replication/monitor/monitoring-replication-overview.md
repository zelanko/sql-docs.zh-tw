---
title: 監視複寫 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], Replication Monitor
- Replication Monitor, about Replication Monitor
ms.assetid: 81f596d2-27a5-489d-bf8d-0f4361decd02
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ae9c89b3fa3d9392e27cce9199f7c1b1b8f31dee
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771420"
---
# <a name="monitoring-replication"></a>監視複寫
  「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器」是一個允許您監視複寫拓撲之全面健全狀況的圖形化工具。 「複寫監視器」提供了發行集和訂閱之狀態和效能的詳細資訊，可讓您回答常見問題，例如：  
  
-   我的複寫系統狀況是否良好？  
  
-   哪些訂閱的速度慢？  
  
-   我的交易式訂閱落後多少？  
  
-   目前一個認可的交易要到達異動複寫中的訂閱者需花多久的時間？  
  
-   為何我的合併訂閱速度很慢？  
  
-   代理程式為何沒有執行？  
  
 若要監視複寫，使用者必須是「散發者」端 **sysadmin** 固定伺服器角色的成員或是散發資料庫中 **replmonitor** 固定資料庫角色的成員。 系統管理員可以將任何使用者新增到 **replmonitor** 角色，此角色允許該使用者在「複寫監視器」中檢視複寫活動；不過，使用者不能管理複寫。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題提供「複寫監視器」功能的資訊。  
  
 [複寫監視器介面概觀](overview-of-the-replication-monitor-interface.md)  
 描述「複寫監視器」中的每個視窗和索引標籤，並提供如何回答以上所列問題的資訊。  
  
 [啟動複寫監視器](start-the-replication-monitor.md)  
 描述如何啟動複寫監視器。  
  
 [允許非管理員使用複寫監視器](allow-non-administrators-to-use-replication-monitor.md)  
 描述如何將權限指派給非管理員，好讓他們可以使用複寫監視器。  
  
 [從複寫監視器新增及移除發行者](add-and-remove-publishers-from-replication-monitor.md)  
 描述如何從複寫監視器加入或移除發行者。  
  
 [在複寫監視器中重新整理資料](refresh-data-in-replication-monitor.md)  
 描述如何重新整理複寫監視器中的資料。  
  
 [使用複寫監視器監視效能](monitor-performance-with-replication-monitor.md)  
 描述如何在「複寫監視器」中監視效能，包括設定效能臨界值的資訊。 包含合併式複寫的發行項層級統計資料之資訊，該統計資料提供處理的詳細檢視。  
  
 [針對異動複寫測量延遲及驗證連接](measure-latency-and-validate-connections-for-transactional-replication.md)  
 描述追蹤 Token，它可讓您測量異動複寫拓撲的效能。  
  
 [監視複寫代理程式](../agents/replication-agents.md)  
 描述如何尋找每個複寫代理程式的資訊。  
  
 [Set Thresholds and Warnings in Replication Monitor](set-thresholds-and-warnings-in-replication-monitor.md)  
 描述可以在「複寫監視器」中設定的警告、臨界值和警示。 建議您啟用拓撲警告，這樣您才能收到即時的狀態和效能資訊。  
  
 [快取、重新整理和複寫監視器效能](caching-refresh-and-replication-monitor-performance.md)  
 描述「複寫監視器」如何快取資料和計算以改善效能；解釋使用者介面的重新整理如何與快取的重新整理相關聯。  
  
 [在複寫監視器中檢視發行集和訂閱狀態](view-publication-and-subscription-status-in-replication-monitor.md)  
 描述如何使用複寫監視器來檢視有關發行或訂閱的狀態資訊。  
  
 [檢視發行者的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
 描述如何使用複寫監視器來檢視資訊以及執行發行者的工作。  
  
 [檢視發行集的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-a-publication-replication-monitor.md)  
 描述如何使用複寫監視器來檢視資訊以及執行發行集的工作。  
  
 [檢視與發行集建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-publication-agents.md)  
 描述如何使用複寫監視器來檢視資訊以及執行與發行集相關聯的代理程式工作。  
  
 [檢視訂閱的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)  
 描述如何使用複寫監視器來檢視資訊以及執行訂閱的工作。  
  
 [檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](view-information-and-perform-tasks-for-subscription-agents.md)  
 描述如何使用複寫監視器來檢視資訊以及執行與訂閱相關聯的代理程式工作。  
  
  
