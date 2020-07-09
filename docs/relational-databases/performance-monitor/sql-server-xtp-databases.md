---
title: SQL Server XTP 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Server 2016 XTP Databases
ms.assetid: 488ff55e-173f-43f6-9bdb-67b35e7cebfe
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f40d6d4afd6195e65ded4e010268251a5bda8b0b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774246"
---
# <a name="sql-server-xtp-databases"></a>SQL Server XTP 資料庫
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**SQL Server XTP Databases** 效能物件提供記憶體內部 OLTP 資料庫特定的計數器。

> [!NOTE]
>  從 sys.dm_os_performance_counters 目前看不到 SQL Server XTP Databases 計數器。  您可以從 [系統監視器](../../relational-databases/performance/start-system-monitor-windows.md)檢視計數器。

下表描述 **SQL Server XTP Databases** 計數器。

|計數器|描述| 
|-------------|-----------------|  
|**Avg Transaction Segment Large Data Size**|交易區段大型資料內容的平均大小。 這是層級非常低的計數器，非供客戶使用。|
|**Avg Transaction Segment Size**|交易區段內容的平均大小。 如果這個值會變成零，則會從後端配置器配置更多頁面。 這是層級非常低的計數器，非供客戶使用。|
|**Flush Thread 256K Queue Depth**|排清 256K IO 要求的執行緒佇列深度。|
|**Flush Thread 4K Queue Depth**|排清 4K IO 要求的執行緒佇列深度。|
|**Flush Thread 64K Queue Depth**|排清 64K IO 要求的執行緒佇列深度。|
|**Flush Thread Frozen IOs/sec (256K)**|在排清頁面處理期間發現高於凍結閾值因此無法發出的 256K IO 要求數目。|
|**Flush Thread Frozen IOs/sec (4K)**|在排清頁面處理期間發現高於凍結閾值因此無法發出的 4K IO 要求數目。|
|**Flush Thread Frozen IOs/sec (64K)**|在排清頁面處理期間發現高於凍結閾值因此無法發出的 64K IO 要求數目。|
|**IoPagePool256K Free List Count**|256K IO 分頁集區可用清單中的分頁數目。 如果這個值會變成零，則會從後端配置器配置更多頁面。 這是層級非常低的計數器，非供客戶使用。|
|**IoPagePool256K Total Allocated**|後端配置器中 256K IO 分頁集區所配置和保留的分頁總數。 這是層級非常低的計數器，非供客戶使用。|
|**IoPagePool4K Free List Count**|4K IO 分頁集區可用清單中的分頁數目。 如果這個值會變成零，則會從後端配置器配置更多頁面。 這是層級非常低的計數器，非供客戶使用。|
|**IoPagePool4K Total Allocated**|後端配置器中 4K IO 分頁集區所配置和保留的分頁總數。 這是層級非常低的計數器，非供客戶使用。|
|**IoPagePool64K Free List Count**|64K IO 分頁集區可用清單中的分頁數目。 如果這個值會變成零，則會從後端配置器配置更多頁面。 這是層級非常低的計數器，非供客戶使用。|
|**IoPagePool64K Total Allocated**|後端配置器中 64K IO 分頁集區所配置和保留的分頁總數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 256K Expand Count**|展開 256K MtLog 的次數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 256K IOs Outstanding**|MtLog 所發出的未完成 256K IO 要求數目。|
|**MtLog 256K Page Fill %/Page Flushed**|排清每個 256K MtLog 分頁的平均填滿百分比。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 256K Write Bytes/sec**|256K MtLog 物件上的每秒寫入位元組數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 4K Expand Count**|展開 4K MtLog 的次數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 4K IOs Outstanding**|MtLog 所發出的未完成 4K IO 要求數目。|
|**MtLog 4K Page Fill %/Page Flushed**|排清每個 4K MtLog 分頁的平均填滿百分比。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 4K Write Bytes/sec**|4K MtLog 物件上的每秒寫入位元組數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 64K Expand Count**|展開 64K MtLog 的次數。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 64K IOs Outstanding**|MtLog 所發出的未完成 64K IO 要求數目。|
|**MtLog 64K Page Fill %/Page Flushed**|排清每個 64K MtLog 分頁的平均填滿百分比。 這是層級非常低的計數器，非供客戶使用。|
|**MtLog 64K Write Bytes/sec**|64K MtLog 物件上的每秒寫入位元組數。 這是層級非常低的計數器，非供客戶使用。|
|**Num Merges**|執行中的合併數目。|
|**Num Merges/sec**|每秒建立的合併數目 (平均)。|
|**Num Serializations**|執行中的序列化數目。|
|**Num Serializations/sec**|每秒建立的序列化數目 (平均)。|
|**Tail Cache Page Count**|結尾快取中所配置的頁數。 這是層級非常低的計數器，非供客戶使用。|
|**Tail Cache Page Count Peak**|結尾快取中所配置的最高頁數。 這是層級非常低的計數器，非供客戶使用。|


## <a name="see-also"></a>另請參閱  
[SQL Server XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
