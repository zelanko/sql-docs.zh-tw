---
title: SQL Server 的 Batch Resp Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 9749469dcec6b15c25f8c517d27b0817ba21c893
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32951663"
---
# <a name="sql-server-batch-resp-statistics-object"></a>SQL Server 的 Batch Resp Statistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**SQLServer:Batch Resp Statistics** 效能物件提供計數器來追蹤 SQL Server 批次回應時間。

下表說明 SQL Server **Batch Resp Statistics** 效能物件。


|**SQL Server Batch Resp Statistics 計數器**|描述|  
|-------------|-----------------|  
|**Batches >=000000ms & \<000001ms**|回應時間大於或等於 0 毫秒但小於 1 毫秒的 SQL 批次數目|
|**Batches >=000001ms & \<000002ms**|回應時間大於或等於 1 毫秒但小於 2 毫秒的 SQL 批次數目|
|**Batches >=000002ms & \<000005ms**|回應時間大於或等於 2 毫秒但小於 5 毫秒的 SQL 批次數目|
|**Batches >=000005ms & \<000010ms**|回應時間大於或等於 5 毫秒但小於 10 毫秒的 SQL 批次數目|
|**Batches >=000010ms & \<000020ms**|回應時間大於或等於 10 毫秒但小於 20 毫秒的 SQL 批次數目|
|**Batches >=000020ms & \<000050ms**|回應時間大於或等於 20 毫秒但小於 50 毫秒的 SQL 批次數目|
|**Batches >=000050ms & \<000100ms**|回應時間大於或等於 50 毫秒但小於 100 毫秒的 SQL 批次數目|
|**Batches >=000100ms & \<000200ms**|回應時間大於或等於 100 毫秒但小於 200 毫秒的 SQL 批次數目|
|**Batches >=000200ms & \<000500ms**|回應時間大於或等於 200 毫秒但小於 500 毫秒的 SQL 批次數目|
|**Batches >=000500ms & \<001000ms**|回應時間大於或等於 500 毫秒但小於 1,000 毫秒的 SQL 批次數目|
|**Batches >=001000ms & \<002000ms**|回應時間大於或等於 1,000 毫秒但小於 2,000 毫秒的 SQL 批次數目|
|**Batches >=002000ms & \<005000ms**|回應時間大於或等於 2,000 毫秒但小於 5,000 毫秒的 SQL 批次數目|
|**Batches >=005000ms & \<010000ms**|回應時間大於或等於 5,000 毫秒但小於 10,000 毫秒的 SQL 批次數目|
|**Batches >=010000ms & \<020000ms**|回應時間大於或等於 10,000 毫秒但小於 20,000 毫秒的 SQL 批次數目|
|**Batches >=020000ms & \<050000ms**|回應時間大於或等於 20,000 毫秒但小於 50,000 毫秒的 SQL 批次數目|
|**Batches >=050000ms & \<100000ms**|回應時間大於或等於 50,000 毫秒但小於 100,000 毫秒的 SQL 批次數目| 
|**Batches >=100000ms**|回應時間大於或等於 100,000 毫秒的 SQL 批次數目| 

物件中的每個計數器均包含下列執行個體：  
  
|項目|描述|  
|----------|-----------------|  
|**CPU Time:Requests**|CPU 花費在要求上的時間。|  
|**CPU Time:Total(ms)**|CPU 花費在批次上的時間總計。|  
|**Elapsed Time:Requests**|要求的經歷時間。|  
|**Elapsed Time:Total(ms)**|批次的經歷時間。|  

## <a name="see-also"></a>另請參閱
[SQL Server 的 Plan Cache 物件](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
