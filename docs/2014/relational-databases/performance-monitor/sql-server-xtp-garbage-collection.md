---
title: XTP 記憶體回收 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5796cc1184e862b4e8afe42b4fa5f5babe8358dd
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52803608"
---
# <a name="xtp-garbage-collection"></a>XTP 記憶體回收
  XTP 記憶體回收效能物件包含與 XTP 引擎記憶體回收行程相關的計數器。  
  
 下表描述**XTP 記憶體回收**計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**塵封角落掃描重試次數/秒 (由 GC 發出)**|記憶體回收行程發出塵封角落掃掠期間，(平均) 每秒因為發生寫入衝突而進行掃描的重試次數。 這是層級非常低的計數器，非供客戶使用。|  
|**主要 GC 工作項目/秒**|主要 GC 執行緒所處理的工作項目數。|  
|**平行 GC 工作項目/秒**|平行執行緒已執行 GC 工作項目的次數。|  
|**已處理的資料列/秒**|記憶體回收行程 (平均) 每秒處理的資料列數目。|  
|**已處理的資料列/秒 (先在貯體中，然後移除)**|記憶體回收行程 (平均) 每秒所處理的資料列數，這些資料列會先在對應的雜湊值區中，並且能夠立即移除。|  
|**已處理的資料列/秒 (先在貯體中)**|記憶體回收行程 (平均) 每秒處理的資料列數，這些資料列會先在對應的雜湊值區中。|  
|**已處理的資料列/秒 (標記為取消連結)**|記憶體回收行程 (平均) 每秒處理的資料列數，這些資料列已標記為取消連結。|  
|**已處理的資料列/秒 (不需要掃掠)**|記憶體回收行程 (平均) 每秒處理的資料列數，這些資料列不需要塵封角落掃掠。|  
|**移除的掃掠過期資料列/秒**|在塵封角落掃掠期間，(平均) 每秒移除的過期資料列數。|  
|**接觸到的掃掠過期資料列/秒**|在塵封角落掃掠期間，(平均) 每秒接觸到的過期資料列數。|  
|**接觸到的掃掠將過期資料列/秒**|在塵封角落掃掠期間，(平均) 每秒接觸到的將過期資料列數。|  
|**接觸到的掃掠資料列/秒**|在塵封角落掃掠期間，(平均) 每秒接觸到的資料列數。|  
|**啟動的掃掠掃描/秒**|(平均) 每秒啟動的塵封角落掃掠掃描次數。|  
  
## <a name="see-also"></a>另請參閱  
 [XTP&#40;記憶體內部 OLTP&#41;效能計數器](../../integration-services/performance/performance-counters.md)  
  
  
