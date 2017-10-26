---
title: "SQL Server XTP IO 管理員 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: 2
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dad1b34551ae96587fafdf3f232ce96b33a96846
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO 管理員
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

SQL Server XTP IO 管理員效能物件包含與記憶體內部 OLTP IO 速率管理員相關的計數器。

本表說明 **SQL Server XTP IO 管理員** 計數器。

|計數器|說明|  
|-------------|-----------------|  
|**Insufficient Credits Waits/sec**|因為速率物件額度不足 (每秒) 所產生的等候次數。|
|**Io Issued/sec**|清除執行緒每秒發出的 Io 數目。|
|**Log Blocks/sec**|控制站每秒處理的記錄區塊數目。|
|**Missed Credit Slots**|因為等候速率物件的信用額度而遺漏的信用插槽數目。|
|**Stale Rate Object Waits/sec**|因為速率物件過時 (每秒) 而產生的等候次數。|
|**Total Rate Objects Published**|發佈的速率物件總數。|
 

## <a name="see-also"></a>另請參閱  
[SQL Server XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)

