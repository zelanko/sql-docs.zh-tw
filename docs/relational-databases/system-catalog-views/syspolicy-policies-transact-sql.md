---
title: syspolicy_policies (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
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
- syspolicy_policies_TSQL
- syspolicy_policies
dev_langs:
- TSQL
helpviewer_keywords:
- syspolicy_policies view
ms.assetid: aecf35bb-187e-4f80-870f-48081b88974e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9ff1b63eae75178c323c731598773ffd53934383
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syspolicypolicies-transact-sql"></a>syspolicy_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，針對每一個以原則為基礎的管理原則各顯示一個資料列。 syspolicy_policies 屬於 msdb 資料庫內的 dbo 結構描述。 下表描述 syspolicy_policies 檢視表中的資料行。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|policy_id|**int**|原則的識別碼。|  
|name|**sysname**|此原則的名稱。|  
|condition_id|**int**|這個原則所強制施行或測試之條件的識別碼。|  
|root_condition_id|**int**|僅供內部使用。|  
|date_created|**datetime**|建立此原則的日期和時間。|  
|execution_mode|**int**|此原則的評估模式。 可能的值如下：<br /><br /> 0 = 視需要<br /><br /> 這種模式會在使用者直接指定時評估原則。<br /><br /> 1 = 變更時: 避免<br /><br /> 這種自動模式會使用 DDL 觸發程序來防止原則違規。<br /><br /> 2 = 變更時: 僅限記錄<br /><br /> 這種自動模式會在發生相關變更時使用事件通知來評估原則，並且記錄原則違規。<br /><br /> 4 = 按排程時間<br /><br /> 這種自動模式會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業來定期評估原則。 此模式會記錄原則違規。<br /><br /> 注意： 3 這個值不是可能的值。|  
|policy_category|**int**|此原則所屬之以原則為基礎之管理原則類別目錄的識別碼。 如果它是預設原則群組，就會是 NULL。|  
|schedule_uid|**uniqueidentifier**|當 execution_mode 為 [按排程時間] 時，會包含此排程的識別碼，否則為 NULL。|  
|description|**nvarchar(max)**|此原則的描述。 描述資料行為選擇性，而且可為 NULL。|  
|help_text|**nvarchar(4000)**|屬於 help_link 的超連結文字。|  
|help_link|**nvarchar(2083)**|由原則建立者指派給原則的其他說明超連結。|  
|object_set_id|**int**|原則評估之物件集的識別碼。|  
|is_enabled|**bit**|指出此原則目前為啟用 (1) 或停用 (0)。|  
|job_id|**uniqueidentifier**|當 execution_mode 為 [按排程時間] 時，會包含執行此原則之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的識別碼。|  
|created_by|**sysname**|建立此原則的登入。|  
|modified_by|**sysname**|最近修改此原則的登入。 如果從未修改過，則為 NULL。|  
|date_modified|**datetime**|建立此原則的日期和時間。 如果從未修改過，則為 NULL。|  
  
## <a name="remarks"></a>備註  
 當您疑難排解原則式管理時，查詢[syspolicy_conditions](../../relational-databases/system-catalog-views/syspolicy-conditions-transact-sql.md)檢視表來判斷是否已啟用原則。 此檢視表也會顯示建立此原則或上次變更此原則的人。  
  
## <a name="permissions"></a>Permissions  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)   
 [以原則為基礎的管理檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
  
  
