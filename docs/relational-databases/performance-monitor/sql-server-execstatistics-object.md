---
title: "SQL Server 的 ExecStatistics 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 709d44983ef7010b36de6238ce99b2d20397017a
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-execstatistics-object"></a>SQL Server 的 ExecStatistics 物件
  Microsoft SQL Server 中的 **SQLServer:ExecStatistics** 物件提供計數器來監視各種執行情形。  
  
 下表描述 SQL Server **Exec Statistics** 計數器。  
  
|SQL Server Exec Statistics 計數器|描述|  
|-----------------------------------------|-----------------|  
|**Distributed Query**|執行分散式查詢的相關統計資料。|  
|**DTC calls**|執行 DTC 呼叫的相關統計資料。|  
|**Extended Procedures**|執行擴充程序的相關統計資料。|  
|**OLEDB calls**|執行 OLEDB 呼叫的相關統計資料。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|項目|描述|  
|----------|-----------------|  
|**平均執行時間 (ms)**|選取的執行類型之平均執行時間。|  
|**每秒累計執行時間 (ms)**|選取的執行類型之每秒彙總執行時間。|  
|**正在執行數目**|選取的執行類型之進行中執行數目。|  
|**每秒開始執行數目**|選取的執行類型之每秒開始的執行數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
