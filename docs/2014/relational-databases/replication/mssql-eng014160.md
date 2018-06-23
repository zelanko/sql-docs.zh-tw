---
title: MSSQL_ENG014160 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014160 error
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0315073cad8a76dea71d3bfce47ad7ebaab0d196
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035418"
---
# <a name="mssqleng014160"></a>MSSQL_ENG014160
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|14160|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|已設定臨界值 [%s:%s] (針對發行集 [%s])。 此發行集的一個或多個訂閱已經到期。|  
  
## <a name="explanation"></a>說明  
 複寫可讓您啟用多個條件的警告。 這包括訂閱即將過期。 如果訂閱在指定 *「保留期限」* 內未執行同步處理，則會使訂閱過期。 如需詳細資訊，請參閱＜ [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)＞。  
  
 使用複寫監視器或 [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql)啟用警告時，您會指定決定何時觸發警告的臨界值。 當達到或超過臨界值時，複寫監視器中會顯示警告，而且會有事件寫入 Windows 事件記錄檔。 達到臨界值也會觸發 SQL Server Agent 警示。 如需詳細資訊，請參閱[在複寫監視器中設定臨界值和警告](monitor/set-thresholds-and-warnings-in-replication-monitor.md)和[以程式設計方式監視複寫](monitor/monitoring-replication-overview.md)。  
  
## <a name="user-action"></a>使用者動作  
 此問題的解決方案需視引發警告的原因而定：  
  
-   如果已超過臨界值，但是訂閱尚未過期，請同步處理訂閱。 如需詳細資訊，請參閱 [同步處理資料](synchronize-data.md)。  
  
-   如果代理程式已經在執行，但未正確複寫變更，可能會導致訂閱過期。 進行異動複寫時，請確認散發代理程式和記錄讀取器代理程式正在執行。 進行合併式複寫時，請確認合併代理程式正在執行。 如需如何啟動這些代理程式的詳細資訊，請參閱[啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 與[複寫代理程式可執行檔概念](concepts/replication-agent-executables-concepts.md)。  
  
-   如果訂閱已過期，則必須重新初始化，或是卸除後再重新建立，需視訂閱類型及已過期時間的長短而定。 如需詳細資訊，請參閱＜ [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
