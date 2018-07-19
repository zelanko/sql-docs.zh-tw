---
title: 記憶體內部 oltp 管理記憶體 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d82f21fa-6be1-4723-a72e-f2526fafd1b6
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09c9d7c759d2cdcd16903ce6e249722cacab3fb5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283814"
---
# <a name="managing-memory-for-in-memory-oltp"></a>為記憶體中的 OLTP 管理記憶體
  記憶體最佳化資料表需要有足夠的記憶體，以將所有資料列和索引保留在記憶體中。 因為記憶體是有限的資源，所以請務必了解並管理系統上的記憶體使用量。 本節的主題涵蓋了常見的記憶體使用與管理案例。  
  
## <a name="in-this-section"></a>本節內容  
  
|章節|描述|  
|-------------|-----------------|  
|[估計記憶體最佳化資料表的記憶體需求](../relational-databases/in-memory-oltp/memory-optimized-tables.md)|估計資料表的記憶體需求。|  
|[將包含記憶體最佳化資料表的資料庫繫結至資源集區](../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)|繫結資料庫與資源集區的逐步解說。|  
|[監視與疑難排解記憶體使用量](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)|您可以用來監視記憶體使用量的工具。 同時也包含記憶體使用量太高的疑難排解方式。|  
|[解決記憶體不足問題](../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md)|從 OOM (記憶體不足) 情況中復原的步驟。|  
|[還原資料庫並將其繫結至資源集區](../relational-databases/in-memory-oltp/restore-a-database-and-bind-it-to-a-resource-pool.md)|還原 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 資料庫並將它繫結至具名資源集區的步驟。|  
|[記憶體內部 OLTP 記憶體回收](../relational-databases/in-memory-oltp/in-memory-oltp-garbage-collection.md)|了解如何對已刪除的資料列進行記憶體回收。|  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
