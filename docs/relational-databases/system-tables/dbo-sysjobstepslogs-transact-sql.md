---
description: dbo.sysjobstepslogs (Transact-SQL)
title: dbo.sysjobstepslogs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 067edf1d3c58df81eac4e49a6ea8d73385d7e21c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544561"
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含設定來將作業步驟輸出寫入資料表中的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟的作業步驟記錄。 此資料表儲存在 **msdb** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|作業步驟記錄的識別碼。|  
|**日誌**|**nvarchar(max)**|作業步驟記錄內容。|  
|**date_created**|**datetime**|作業步驟記錄的建立日期和時間。|  
|**date_modified**|**datetime**|上次修改作業步驟記錄的日期和時間。|  
|**log_size**|**int**|作業步驟記錄的大小 (以位元組為單位)。|  
|**step_uid**|**uniqueidentifier**|作業步驟的唯一識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_jobsteplog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
