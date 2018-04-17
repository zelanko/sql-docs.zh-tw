---
title: syspolicy_policy_execution_history_details (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syspolicy_policy_execution_history_details
- syspolicy_policy_execution_history_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policy_execution_history_details view
ms.assetid: 97ef6573-5e8b-4ba5-8ae0-7901e79a9683
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2db4cae845b3fae42501a2a56d9218d47bc07fc7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syspolicypolicyexecutionhistorydetails-transact-sql"></a>syspolicy_policy_execution_history_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示已執行的條件運算式、運算式的目標、每一次執行的結果，以及任何發生之錯誤的相關詳細資料。 下表描述 syspolicy_execution_history_details 檢視表中的資料行。  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|detail_id|**bigint**|這筆記錄的識別碼。 每一筆記錄都表示嘗試評估或強制施行原則中的某一個條件運算式。 如果套用到多個目標，每一個條件都將會有每一個目標的詳細記錄。|  
|history_id|**bigint**|記錄事件的識別碼。 每一個記錄事件都表示執行原則的某個嘗試。 由於一個條件可以有數個條件運算式及數個目標，所以 history_id 可以建立幾筆詳細記錄。 使用 history_id 資料行來聯結此檢視來[syspolicy_policy_execution_history](../../relational-databases/system-catalog-views/syspolicy-policy-execution-history-transact-sql.md)檢視。|  
|target_query_expression|**nvarchar(max)**|此原則和 syspolicy_policy_execution_history 檢視表的目標。|  
|execution_date|**datetime**|建立這筆詳細記錄的日期和時間。|  
|result|**bit**|這個目標和條件運算式評估為成功或失敗：<br /><br /> 0 (成功) 或 1 (失敗)。|  
|result_detail|**nvarchar(max)**|結果訊息。 只有當此 Facet 提供時才可用。|  
|exception_message|**nvarchar(max)**|由發生的例外狀況所產生的訊息。|  
|exception|**nvarchar(max)**|發生之例外狀況的描述。|  
  
## <a name="remarks"></a>備註  
 當您針對以原則為基礎的管理進行疑難排解時，請查詢 syspolicy_policy_execution_history_details 檢視表來判斷哪一個目標和條件運算式組合失敗、其失敗的時間，並檢閱相關錯誤。  
  
 下列查詢會將 `syspolicy_policy_execution_history_details` 檢視表與 `syspolicy_policy_execution_history_details` 和 `syspolicy_policies` 檢視表結合，以顯示此原則的名稱、此條件的名稱及有關失敗的詳細資料。  
  
```  
SELECT Pol.name AS Policy,   
Cond.name AS Condition,   
PolHistDet.target_query_expression,   
PolHistDet.execution_date,   
PolHistDet.result,   
PolHistDet.result_detail,   
PolHistDet.exception_message,   
PolHistDet.exception   
FROM msdb.dbo.syspolicy_policies AS Pol  
JOIN msdb.dbo.syspolicy_conditions AS Cond  
    ON Pol.condition_id = Cond.condition_id  
JOIN msdb.dbo.syspolicy_policy_execution_history AS PolHist  
    ON Pol.policy_id = PolHist.policy_id  
JOIN msdb.dbo.syspolicy_policy_execution_history_details AS PolHistDet  
    ON PolHist.history_id = PolHistDet.history_id  
WHERE PolHistDet.result = 0 ;  
```  
  
## <a name="permissions"></a>Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
