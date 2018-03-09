---
title: "sysdbmaintplans (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6297a26f046c82b628bc65de8131bc21dd6f59fd
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此資料表包含於[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]保留的現有資訊的執行個體會將升級從舊版的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會變更此資料表的內容。 這份資料表儲存在**msdb**資料庫。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|資料庫維護計畫識別碼。|  
|**plan_name**|**sysname**|資料庫維護計畫名稱。|  
|**date_created**|**datetime**|資料庫維護計畫的建立日期。|  
|**擁有者**|**sysname**|資料庫維護計畫的擁有者。|  
|**max_history_rows**|**int**|用來將資料庫維護計畫的記錄記載到系統資料表中，所配置的最大資料列數。|  
|**remote_history_server**|**sysname**|可寫入記錄報表之遠端伺服器的名稱。|  
|**max_remote_history_rows**|**int**|在遠端伺服器系統資料表中，可寫入記錄報表的資料列最大配置列數。|  
|**user_defined_1**|**int**|預設值是 NULL。|  
|**user_defined_2**|**nvarchar(100)**|預設值是 NULL。|  
|**user_defined_3**|**datetime**|預設值是 NULL。|  
|**user_defined_4**|**uniqueidentifier**|預設值是 NULL。|  
|**log_shipping**|**bit**|記錄傳送狀態：<br /><br /> **0** = 已停用**1** = 啟用|  
  
  
