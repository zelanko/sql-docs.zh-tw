---
title: "MSagent_profiles (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs: TSQL
helpviewer_keywords: MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a5423c227bd16008e08bc3a70f25dd899e392f5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="msagentprofiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_profiles**資料表包含一個資料列，每個定義的複寫代理程式設定檔。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|設定檔識別碼。|  
|**profile_name**|**sysname**|代理程式類型的唯一設定檔名稱。|  
|**agent_type**|**int**|代理程式的類型：<br /><br /> **1** = 快照集代理程式<br /><br /> **2** = 記錄讀取器代理程式<br /><br /> **3** = 散發代理程式<br /><br /> **4** = 合併代理程式<br /><br /> **9** = 佇列讀取器代理程式|  
|**型別**|**int**|設定檔的類型：<br /><br /> **0** = 系統**1** = 自訂|  
|**描述**|**nvarchar （3000)**|設定檔的描述。|  
|**def_profile**|**bit**|指定這個設定檔是否為這個代理程式類型的預設值。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
