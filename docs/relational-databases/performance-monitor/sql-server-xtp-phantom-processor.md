---
title: "SQL Server XTP 虛設處理器 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 722137db4fdddd79f8ed4bfe8d5a7c3ed4531738
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-xtp-phantom-processor"></a>SQL Server XTP 虛設項目處理器
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP 虛設項目處理器效能物件包含與記憶體內部 OLTP 引擎的虛設項目處理子系統相關的計數器。 此元件負責偵測在 SERIALIZABLE 隔離等級執行之交易中的虛設項目列，以及並行案例中的條件約束驗證。  
  
 下表描述 **SQL Server XTP 虛設項目處理器** 計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**塵封角落掃描重試次數/秒 (由虛設項目發出)**|虛設處理器發出塵封角落掃掠期間，(平均) 每秒因為發生寫入衝突而進行掃描的重試次數。 這是層級非常低的計數器，非供客戶使用。|  
|**移除的虛設過期資料列/秒**|(平均) 每秒虛設掃描移除的過期資料列數。|  
|**接觸到的虛設過期資料列/秒**|(平均) 每秒虛設掃描接觸到的過期資料列數。|  
|**接觸到的虛設將過期資料列/秒**|(平均) 每秒虛設掃描接觸到的將過期資料列數。|  
|**接觸到的虛設項目列/秒**|(平均) 每秒虛設掃描接觸到的資料列數。|  
|**啟動的虛設掃描/秒**|(平均) 每秒啟動的虛設掃描次數。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
