---
title: dbo.sysschedules (TRANSACT-SQL) |Microsoft 文件
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
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2818512730a99bf7352c87f7d651d3084870767f
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "33252703"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行之作業的排程資訊。 這份資料表儲存在**msdb**資料庫。  
  
> **注意：** **sysjobschedules**資料表重新整理每隔 20 分鐘，這可能會影響傳回的值**sp_help_jobschedule**預存程序。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|排程的識別碼。|  
|**job_id**|**uniqueidentifier**|作業的識別碼。|  
|**next_run_date**|**int**|排程下一次執行作業的日期。 日期格式為 YYYYMMDD。|  
|**next_run_time**|**int**|排程執行作業的時間。 時間格式為 HHMMSS，使用 24 小時制。|  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysjobschedules &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
