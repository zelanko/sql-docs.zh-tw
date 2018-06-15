---
title: _ S c h (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MSsubscriber_schedule
- MSsubscriber_schedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_schedule system table
ms.assetid: ff428306-0ef4-49a3-b536-07ccdf6e2196
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e38c0d789862bc0e2464c74e0ff0ba438c32ffb3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33011115"
---
# <a name="mssubscriberschedule-transact-sql"></a>MSsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscriber_schedule**資料表包含預設合併和交易式同步處理的每個發行者/訂閱者組的排程。 這份資料表儲存在散發資料庫中。  
  
> [!NOTE]  
>  這個系統資料表已被取代，而且正加以維護，以支援舊版的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|發行者的名稱。|  
|**訂閱者**|**sysname**|訂閱者的名稱。|  
|**agent_type**|**smallint**|代理程式的類型：<br /><br /> 0 = 散發代理程式。<br /><br /> 1 = 合併代理程式。|  
|**frequency_type**|**int**|排程散發代理程式所採用的頻率：<br /><br /> **1** = 一次。<br /><br /> **2** = 視。<br /><br /> **4** = 每天。<br /><br /> **8** = 每週。<br /><br /> **16** = 每月。<br /><br /> **32** = 每月相對。<br /><br /> **64** = 自動啟動。<br /><br /> **128** = 重複執行。|  
|**frequency_interval**|**int**|若要設定的頻率所套用的值**frequency_type**。|  
|**frequency_relative_interval**|**int**|散發代理程式的日期：<br /><br /> **1** = 第一個。<br /><br /> **2** = 第二個。<br /><br /> **4** = 第三個。<br /><br /> **8** = 第四個。<br /><br /> **16** = 最後一個。|  
|**frequency_recurrence_factor**|**int**|所用的循環因數**frequency_type**。|  
|**frequency_subday**|**int**|在定義的期間內，重新排程的頻率：<br /><br /> **1** = 一次。<br /><br /> **2** = 第二個。<br /><br /> **4** = 分。<br /><br /> **8** = 小時。|  
|**frequency_subday_interval**|**int**|間隔**frequency_subday**。|  
|**active_start_time_of_day**|**int**|第一次排程散發代理程式的當日時間，格式為 HHMMSS。|  
|**active_end_time_of_day**|**int**|停止排程散發代理程式的當日時間，格式為 HHMMSS。|  
|**active_start_date**|**int**|第一次排程散發代理程式的日期，格式為 YYYYMMDD。|  
|**active_end_date**|**int**|停止排程散發代理程式的日期，格式為 YYYYMMDD。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
