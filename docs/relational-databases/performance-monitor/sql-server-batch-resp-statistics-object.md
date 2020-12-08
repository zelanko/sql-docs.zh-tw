---
title: SQL Server 的 Batch Resp Statistics 物件 | Microsoft Docs
description: 了解 SQLServer:Batch Resp Statistics 效能物件，其提供計數器來追蹤 SQL Server 批次回應時間。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: acd7dc7b853c600b743d9791a3bade6ce8970a41
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505862"
---
# <a name="sql-server-batch-resp-statistics-object"></a>SQL Server 的 Batch Resp Statistics 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
|**CPU Time:Requests**|根據 CPU 時間的要求數。|  
|**CPU Time:Total(ms)**|CPU 花費在批次上的時間總計。|  
|**Elapsed Time:Requests**|根據已耗用時間的要求數。|  
|**Elapsed Time:Total(ms)**|批次的經歷時間。|  

## <a name="see-also"></a>另請參閱
[SQL Server 的 Plan Cache 物件](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[監視資源使用狀況 (系統監視器)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
