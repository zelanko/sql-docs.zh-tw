---
title: syspolicy_policy_execution_history (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_TSQL
- syspolicy_policy_execution_history
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history view
ms.assetid: b13c44a7-6d49-4d50-abe1-e657fc52bb05
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5d21894663f8ad36a44e825a1b0e8ced4966ee8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33220319"
---
# <a name="syspolicypolicyexecutionhistory-transact-sql"></a>syspolicy_policy_execution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示原則執行的時間、每一次執行的結果，以及任何發生之錯誤的相關詳細資料。 下表描述 syspolicy_policy_execution_history 檢視表中的資料行。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|history_id|**bigint**|這筆記錄的識別碼。 每一筆記錄都會指示一個原則，以及此原則之前起始的一個時間。|  
|policy_id|**int**|原則的識別碼。|  
|start_date|**datetime**|此原則之前嘗試執行的日期和時間。|  
|end_date|**datetime**|此原則完成執行的時間。|  
|result|**bit**|此原則為成功或失敗。 0 = 失敗，1 = 成功。|  
|exception_message|**nvarchar(max)**|由發生的例外狀況所產生的訊息。|  
|exception|**nvarchar(max)**|發生之例外狀況的描述。|  
  
## <a name="remarks"></a>備註  
 [Syspolicy_policy_execution_history_details](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-details-transact-sql.md)檢視包含有關原則與測試之條件運算式的目標的相關詳細資料。  
  
## <a name="permissions"></a>Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
