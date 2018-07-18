---
title: SQL Server 的 Query Store 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 527ad5bc399654bd69a05bbca4f801e7c6d643ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32951163"
---
# <a name="sql-server-query-store-object"></a>SQL Server, 查詢存放區物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  查詢存放區物件所提供的計數器，可監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何使用資源來儲存查詢文字、執行計劃和物件的執行階段統計資料，例如預存程序、特定與備妥 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以及觸發程序。  
  
 下表描述 **SQLServer:Query Store**計數器。  
  
|SQL Server 查詢存放區計數器|描述|  
|-------------------------------------|-----------------|  
|**查詢存放區 CPU 使用量**|表示 CPU 的查詢存放區使用量。|  
|**查詢存放區邏輯讀取**|表示查詢存放區所做的邏輯讀取數。|  
|**查詢存放區邏輯寫入**|表示查詢存放區中有多少資料佇列以進行排清。 將項目新增至佇列的的頻率和延遲 (代表執行階段統計資料) 是由資料排清間隔設定所控制。|  
|**查詢存放區實體讀取**|表示查詢存放區所做的實體讀取數。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|查詢存放區執行個體|描述|  
|--------------------------|-----------------|  
|**_Total**|此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的查詢存放區資訊。|  
|\<資料庫名稱>|此資料庫的查詢存放區資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [查詢存放區目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
