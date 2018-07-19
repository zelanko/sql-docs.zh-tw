---
title: SQL Server XTP 交易 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a9da78f30f38fb5cbb72e573497f93a138fec37e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32950993"
---
# <a name="sql-server-xtp-transactions"></a>SQL Server XTP 交易
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  SQL Server XTP Transactions 效能物件包含與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中記憶體內部 OLTP 交易相關的計數器。  
  
 下表描述 **SQL Server XTP Transactions** 計數器。  
  
|計數器|描述|  
|-------------|-----------------|  
|**串聯中止/秒**|(平均) 每秒因為認可相依性回復而回復的交易數。|  
|**採取的認可相依性/秒**|(平均) 每秒交易採取的認可相依性數目。|  
|**準備的唯讀交易/秒**|每秒為了認可處理而準備的唯讀交易數。|  
|**儲存點重新整理/秒**|(平均) 每秒儲存點「重新整理」的次數。 儲存點重新整理是指在交易存留期間，將現有儲存點重設為目前點的時候。|  
|**儲存點回復/秒**|(平均) 每秒交易回復到儲存點的次數。|  
|**建立的儲存點/秒**|(平均) 每秒建立的儲存點數。|  
|**交易驗證失敗/秒**|(平均) 每秒驗證處理失敗的交易數。|  
|**使用者中止的交易/秒**|(平均) 每秒使用者中止的交易數。|  
|**中止的交易/秒**|(平均) 每秒中止的交易數，包括由使用者和系統中止的數目。|  
|**建立的交易/秒**|(平均) 每秒在系統中建立的交易數目。<br /><br /> XTP 交易的計數方式跟磁碟交易不同 (如 Databases:Transactions/sec 中所反映)。 例如，Transactions created/sec 是計算唯讀交易，Databases:Transactions/sec 則不是。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server XTP &#40;記憶體內部 OLTP&#41; 效能計數器](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
