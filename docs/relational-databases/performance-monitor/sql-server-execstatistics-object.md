---
title: SQL Server 的 ExecStatistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 054ff1d108a958e40a17a2316377559295746e7b
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380023"
---
# <a name="sql-server-execstatistics-object"></a>SQL Server 的 ExecStatistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft SQL Server 中的 **SQLServer:ExecStatistics** 物件提供計數器來監視各種執行情形。  
  
 下表描述 SQL Server **Exec Statistics** 計數器。  
  
|SQL Server Exec Statistics 計數器|Description|  
|-----------------------------------------|-----------------|  
|**Distributed Query**|執行分散式查詢的相關統計資料。|  
|**DTC calls**|執行 DTC 呼叫的相關統計資料。|  
|**Extended Procedures**|執行擴充程序的相關統計資料。|  
|**OLEDB calls**|執行 OLEDB 呼叫的相關統計資料。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|項目|Description|  
|----------|-----------------|  
|**平均執行時間 (ms)**|選取的執行類型之平均執行時間。|  
|**每秒累計執行時間 (ms)**|選取的執行類型之每秒彙總執行時間。|  
|**正在執行數目**|選取的執行類型之進行中執行數目。|  
|**每秒開始執行數目**|選取的執行類型之每秒開始的執行數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
