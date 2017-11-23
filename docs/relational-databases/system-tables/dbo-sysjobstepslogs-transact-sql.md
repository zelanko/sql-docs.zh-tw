---
title: "dbo.sysjobstepslogs (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs: TSQL
helpviewer_keywords: sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 050feecde1f82ca8962552744e2fc2d43d28bd4c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含設定來將作業步驟輸出寫入資料表中的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟的作業步驟記錄。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**g _ i d**|**int**|作業步驟記錄的識別碼。|  
|**記錄檔**|**nvarchar(max)**|作業步驟記錄內容。|  
|**date_created**|**datetime**|作業步驟記錄的建立日期和時間。|  
|**date_modified**|**datetime**|上次修改作業步驟記錄的日期和時間。|  
|**log_size**|**int**|作業步驟記錄的大小 (以位元組為單位)。|  
|**step_uid**|**uniqueidentifier**|作業步驟的唯一識別碼。|  
  
## <a name="see-also"></a>請參閱＜  
 [sp_help_jobsteplog &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
