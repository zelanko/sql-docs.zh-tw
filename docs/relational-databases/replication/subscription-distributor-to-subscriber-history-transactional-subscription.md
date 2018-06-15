---
title: 訂閱，散發者到訂閱者記錄 (交易式訂閱) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.disttosub.f1
ms.assetid: 1aad5b82-592e-4907-92f7-b90794175be5
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 775a138a247c875eb04b3ca843f11e1bfea54dff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32961963"
---
# <a name="subscription-distributor-to-subscriber-history-transactional-subscription"></a>訂閱，散發者到訂閱者記錄 (交易式訂閱)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **[散發者到訂閱者記錄]** 索引標籤會顯示散發代理程式的詳細資訊，包括狀態、記錄、參考訊息和錯誤訊息。  
  
## <a name="options"></a>選項。  
 從 **[檢視]** 功能表中選取要檢視的散發代理程式工作階段，再於 **[散發代理程式的工作階段]** 的方格中選取特定的工作階段。 有關這個工作階段的詳細資訊，會顯示在標示為 **[所選取工作階段中的動作]** 之方格中。 如果選取的工作階段結束時發生錯誤， **[所選取之工作階段的錯誤詳細資料或訊息]** 的文字區域也會顯示。  
  
 **[檢視]**  
 選取要檢視的散發代理程式工作階段。 散發代理程式通常會連續執行，因此可能只有一個工作階段可檢視。  
  
 **狀態**  
 散發代理程式的狀態。 下列清單顯示可能的狀態值：  
  
-   錯誤  
  
-   已完成  
  
-   正在重試  
  
-   執行中  
  
 **Start Time**  
 工作階段的開始時間。  
  
 **結束時間**  
 工作階段的結束時間。 如果代理程式未停止，則這個欄位是空的。  
  
 **有效期間**  
 散發代理程式在這個工作階段中執行的時間量。 如果代理程式目前正在執行，則時間代表經過時間，如果代理程式工作階段已結束，則時間代表工作階段總共花費的時間。  
  
 **錯誤訊息**  
 如果工作階段結束時發生錯誤，這個欄位會顯示散發代理程式記錄的最後一個錯誤訊息。 如果工作階段結束時沒有錯誤，這個欄位會是空白。  
  
 **動作訊息**  
 散發代理程式在所選取工作階段期間，記錄的所有參考訊息和錯誤訊息。  
  
 **動作時間**  
 執行 **[動作訊息]** 資料行所描述之動作的時間。  
  
 **[所選取之工作階段的錯誤詳細資料或訊息]**  
 唯有所選取工作階段在 **[狀態]** 資料行中顯示的值為 **[錯誤]** 時，才會顯示。 此文字區域會顯示詳細錯誤資訊和發生錯誤時所嘗試的命令。 它也會包括與錯誤相關之其他內容的連結。  
  
## <a name="see-also"></a>另請參閱  
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [檢視與訂閱建立關聯之代理程式的資訊並執行工作 &#40;複寫監視器&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
