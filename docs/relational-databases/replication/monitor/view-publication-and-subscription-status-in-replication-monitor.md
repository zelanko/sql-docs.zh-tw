---
title: 檢視發行集與訂閱狀態 (複寫監視器)
description: 了解如何在 SQL Server Management Studio (SSMS) 中使用複寫監視器來檢視發行集和訂閱狀態。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, monitoring
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- publications [SQL Server replication], viewing information
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication], publication status
- monitoring performance [SQL Server replication], subscription status
- subscriptions [SQL Server replication], viewing status
- Replication Monitor, publication and subscription status
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3e9353cc5d22cae0f148661ca5a31651803bc00e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286353"
---
# <a name="view-publication-and-subscription-status-in-replication-monitor"></a>在複寫監視器中檢視發行集和訂閱狀態
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫監視器會顯示發行集和訂閱的狀態資訊：  
  
-   發行集的狀態是由其訂閱的最高優先權狀態所決定。 例如，如果發行集的某個訂閱發生錯誤，而另一個訂閱發生效能問題，則會針對該發行集顯示錯誤狀態。  
  
-   訂閱的狀態是由服務訂閱的代理程式狀態所決定。 對於合併複寫來說，這是指「合併代理程式」。 對於異動複寫來說，這是指「記錄讀取器代理程式」或「散發代理程式」(會顯示較高優先權的狀態；而如果使用佇列更新訂閱，狀態亦可由「佇列讀取器代理程式」決定)。 對於快照集複寫來說，這是指「快照集代理程式」或「散發代理程式」(會顯示較高優先權的狀態)。  
  
 下列各節中的資料表會列出發行集和訂閱的可能狀態值。 這三種狀態值只會在達到或超過臨界值時顯示：  
  
-   訂閱過期  
  
     這個狀態值適用所有複寫類型。 如需相關資訊，請參閱 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
-   效能嚴重不足  
  
     這個狀態值適用異動複寫和合併複寫。 如需詳細資訊，請參閱[使用複寫監視器監視效能](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
-   長期執行合併  
  
     這個狀態值適用合併複寫。 如需詳細資訊，請參閱[使用複寫監視器監視效能](../../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)。  
  
 除了發行集和訂閱狀態之外，合併複寫還提供發行項層級的統計資料，其中提供的詳細資訊包括：合併階段需花多長的時間完成、已花費多少時間處理指定的發行項、「訂閱者」使用的連接類型，以及其他重要資訊。 統計資料會在「複寫監視器」的「合併代理程式」視窗中顯示。 快照集和異動複寫會提供有關「散發代理程式」處理的詳細資訊。  
  
 **檢視發行集和訂閱狀態**  
  
-   複寫監視器：[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md) 
  
 **檢視代理程式的詳細資訊**  
  
-   複寫監視器：[使用複寫監視器來檢視資訊及執行工作](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)。
  
## <a name="publication-status-values"></a>發行集狀態值  
 下表按優先權順序顯示發行集狀態值及其對應的圖示。  
  
|狀態|圖示|  
|------------|----------|  
|錯誤|![UI 圖示：錯誤](../../../database-engine/availability-groups/windows/media/repl-icon-error.gif "UI 圖示：錯誤")|  
|效能嚴重不足|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|正在重試失敗的命令|![UI 圖示：複寫代理程式重試](../../../relational-databases/replication/monitor/media/repl-icon-retry.gif "UI 圖示：複寫代理程式重試")|  
|[確定]|無|  
  
## <a name="subscription-status-values"></a>訂閱狀態值  
 下列各資料表按優先權順序顯示訂閱狀態值及其對應的圖示。 訂閱可同時處於兩種狀態，例如 **「即將過期/已過期」** 和 **「正在重試失敗的命令」** ；此時會顯示最高優先權的狀態。  
  
 **「效能嚴重不足」** 、 **「即將過期/已過期」** 和 **「未初始化」** 等狀態值都是警告。 當顯示警告時，「複寫監視器」也會顯示是否有代理程式正在執行。 例如，狀態可能是 **[執行中，效能嚴重不足]** 。  
  
### <a name="transactional-subscriptions"></a>交易式訂閱  
  
|狀態|圖示|  
|------------|----------|  
|錯誤|![UI 圖示：錯誤](../../../database-engine/availability-groups/windows/media/repl-icon-error.gif "UI 圖示：錯誤")|  
|效能嚴重不足|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|「即將過期/已過期」|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|未初始化的訂閱|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|正在重試失敗的命令|![UI 圖示：複寫代理程式重試](../../../relational-databases/replication/monitor/media/repl-icon-retry.gif "UI 圖示：複寫代理程式重試")|  
|未執行|![UI 圖示：複寫代理程式已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.gif "UI 圖示：複寫代理程式已停止")|  
|執行中|![UI 圖示：複寫代理程式執行中](../../../relational-databases/replication/monitor/media/repl-icon-running.gif "UI 圖示：複寫代理程式執行中")|  
  
### <a name="merge-subscriptions"></a>合併訂閱  
  
|狀態|圖示|  
|------------|----------|  
|錯誤|![UI 圖示：錯誤](../../../database-engine/availability-groups/windows/media/repl-icon-error.gif "UI 圖示：錯誤")|  
|效能嚴重不足|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|長期執行合併|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|「即將過期/已過期」|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|未初始化的訂閱|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|正在重試失敗的命令|![UI 圖示：複寫代理程式重試](../../../relational-databases/replication/monitor/media/repl-icon-retry.gif "UI 圖示：複寫代理程式重試")|  
|正在同步處理|![UI 圖示：複寫代理程式執行中](../../../relational-databases/replication/monitor/media/repl-icon-running.gif "UI 圖示：複寫代理程式執行中")|  
|未進行同步處理|![UI 圖示：複寫代理程式已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.gif "UI 圖示：複寫代理程式已停止")|  
  
### <a name="snapshot-subscriptions"></a>快照集訂閱  
  
|狀態|圖示|  
|------------|----------|  
|錯誤|![UI 圖示：錯誤](../../../database-engine/availability-groups/windows/media/repl-icon-error.gif "UI 圖示：錯誤")|  
|「即將過期/已過期」|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|未初始化的訂閱|![UI 圖示：警告](../../../database-engine/availability-groups/windows/media/repl-icon-warn.gif "UI 圖示：警告")|  
|正在重試失敗的命令|![UI 圖示：複寫代理程式重試](../../../relational-databases/replication/monitor/media/repl-icon-retry.gif "UI 圖示：複寫代理程式重試")|  
|正在同步處理|![UI 圖示：複寫代理程式執行中](../../../relational-databases/replication/monitor/media/repl-icon-running.gif "UI 圖示：複寫代理程式執行中")|  
|未進行同步處理|![UI 圖示：複寫代理程式已停止](../../../relational-databases/replication/monitor/media/repl-icon-stopped.gif "UI 圖示：複寫代理程式已停止")|  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
