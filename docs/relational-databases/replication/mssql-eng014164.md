---
title: MSSQL_ENG014164 | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014164 error
ms.assetid: cd81b601-2ec3-4358-ad58-c2655496e6a1
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c52686b7bf59eeab5b9c87eb6b6f3f7d2a58caf5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng014164"></a>MSSQL_ENG014164
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|14164|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|已設定臨界值 [%s:%s]\(針對發行集 [%s])。 請確定合併代理程式正在執行，而且符合預期需求。|  
  
## <a name="explanation"></a>說明  
 複寫可讓您啟用多個條件的警告。 這包括在同步處理合併發行者與訂閱者之間的變更時，無法處理足夠數量的資料列的情況。 您可以為 LAN 連接和撥號連接指定不同的時間。  
  
 使用複寫監視器或 [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)啟用警告時，您會指定決定何時觸發警告的臨界值。 當達到或超過臨界值時，複寫監視器中會顯示警告，而且會有事件寫入 Windows 事件記錄檔。 達到臨界值也會觸發 SQL Server Agent 警示。 如需詳細資訊，請參閱[在複寫監視器中設定臨界值和警告](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[以程式設計方式監視複寫](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)。  
  
## <a name="user-action"></a>使用者動作  
 如果訂閱不符合資料列處理臨界值，則必須判斷是否發生系統效能問題，或者應該調整臨界值。 在設定複寫後，請開發效能基準線，以便決定複寫對應用程式及拓撲一般工作負載的操作方式。 請將已處理的資料列數包含在此基準線中，以便設定適當的臨界值。  
  
 如果臨界值適當，但是即將超過，您就必須判斷系統的效能瓶頸何在。 如需有關如何監視與疑難排解複寫效能的詳細資訊，請參閱下列主題：  
  
-   [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) (特別是＜檢視合併式複寫的詳細同步處理效能＞一節)  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  

