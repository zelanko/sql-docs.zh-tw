---
title: dbo.sysjobschedules (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 877abbc8fb58fbb3a824bb711e0adbb13618f453
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262825"
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業排程的相關資訊。 這份資料表儲存在**msdb**資料庫。  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業排程的識別碼。|  
|**schedule_uid**|**uniqueidentifier**|作業排程的唯一識別碼。 這個值用來識別分散式作業的排程。|  
|**originating_server_id**|**int**|作業排程的來源主要伺服器識別碼。|  
|**name**|**sysname (nvarchar(128))**|作業排程的使用者自訂名稱。 這個名稱在作業內必須是唯一的。|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*的使用者或群組擁有作業排程。|  
|**enabled**|**int**|作業排程的狀態：<br /><br /> **0** = 未啟用。<br /><br /> **1** = 啟用。<br /><br /> 如果未啟用排程，便不會依據這份排程來執行任何作業。|  
|**freq_type**|**int**|針對這份排程來執行作業的頻率。<br /><br /> **1** = 只一次<br /><br /> **4** = 每天<br /><br /> **8** = 每週<br /><br /> **16** = 每月<br /><br /> **32** = 每月，相對於**freq_interval**<br /><br /> **64** = SQL Server Agent 服務啟動時執行<br /><br /> **128** = 時電腦閒置時執行|  
|**freq_interval**|**int**|執行作業的天數。 值而定**freq_type**。 預設值是**0**，這表示**freq_interval**未使用。 請參閱下方的資料表可能的值和其效果。|  
|**freq_subday_type**|**int**|單位**freq_subday_interval**。 以下是可能的值和它們的描述。<br /><br /> <br /><br /> **1** ： 在指定的時間<br /><br /> **2** ： 秒<br /><br /> **4** ： 分鐘<br /><br /> **8** ： 時數|  
|**freq_subday_interval**|**int**|數目**freq_subday_type**期間每次執行作業之間發生。|  
|**freq_relative_interval**|**int**|當**freq_interval**如果就會發生在每月**freq_interval**是**32** （每月相對）。 可以是下列其中一個值：<br /><br /> **0** = **freq_relative_interval**未使用<br /><br /> **1** = 第一個<br /><br /> **2** = 第二個<br /><br /> **4** = 第三個<br /><br /> **8** = 第四個<br /><br /> **16** = 最後一個|  
|**freq_recurrence_**<br /><br /> **factor**|**int**|作業的排程執行之間的週數或月數。 **freq_type**才會使用**freq_type**是**8**， **16**，或**32**。 如果此資料行包含**0**， **freq_type**未使用。|  
|**active_start_date**|**int**|可以開始執行作業的日期。 日期格式為 YYYYMMDD。 NULL 表示今天的日期。|  
|**active_end_date**|**int**|可以停止執行作業的日期。 日期格式為 YYYYMMDD。|  
|**active_start_time**|**int**|之間任何一天時間**active_start_date**和**active_end_date**開始執行該作業。 時間格式為 HHMMSS，使用 24 小時制。|  
|**active_end_time**|**int**|之間任何一天時間**active_start_date**和**active_end_date**停止執行該作業。 時間格式為 HHMMSS，使用 24 小時制。|  
|**date_created**|**datetime**|排程的建立日期和時間。|  
|**date_modified**|**datetime**|上次修改排程的日期和時間。|  
|**version_number**|**int**|排程的目前版本號碼。 例如，如果排程修改過 10 次， **version_number**為 10。|  
  
|freq_type 的值|freq_interval 的作用|  
|-------------------------|------------------------------|  
|**1** （一次）|**freq_interval**未使用 (**0**)|  
|**4** （每天）|每個**freq_interval**天|  
|**8** （每週）|**freq_interval**是下列一或多個項目：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **4** = 星期二<br /><br /> **8** = 星期三<br /><br /> **16** = 星期四<br /><br /> **32** = 星期五<br /><br /> **64** = 星期六|  
|**16** （每月）|在**freq_interval**每月的日|  
|**32** （每月，相對）|**freq_interval**是下列其中之一：<br /><br /> **1** = 星期日<br /><br /> **2** = 星期一<br /><br /> **3** = 星期二<br /><br /> **4** = 星期三<br /><br /> **5** = 星期四<br /><br /> **6** = 星期五<br /><br /> **7** = 星期六<br /><br /> **8** = 日<br /><br /> **9** = 工作日<br /><br /> **10** = 週末|  
|**64** （SQL Server Agent 服務啟動時啟動）|**freq_interval**未使用 (**0**)|  
|**128** （在電腦閒置時執行）|**freq_interval**未使用 (**0**)|  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysschedules & #40;TRANSACT-SQL & #41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
