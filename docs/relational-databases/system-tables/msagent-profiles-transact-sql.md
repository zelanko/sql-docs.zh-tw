---
title: MSagent_profiles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5147ef1f482850b55a5d01a476b1981dfa012e5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68021058"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSagent_profiles**資料表會針對每個定義的複寫代理程式設定檔，各包含一個資料列。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|設定檔識別碼。|  
|**profile_name**|**sysname**|代理程式類型的唯一設定檔名稱。|  
|**agent_type**|**int**|代理程式的類型：<br /><br /> **1** = 快照集代理程式<br /><br /> **2** = 記錄讀取器代理程式<br /><br /> **3** = 散發代理程式<br /><br /> **4** = 合併代理程式<br /><br /> **9** = 佇列讀取器代理程式|  
|**type**|**int**|設定檔的類型：<br /><br /> **0** = 系統**1** = 自訂|  
|**描述**|**Nvarchar （3000）**|設定檔的描述。|  
|**def_profile**|**bit**|指定這個設定檔是否為這個代理程式類型的預設值。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
