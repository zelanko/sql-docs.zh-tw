---
title: sys.syslogins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslogins_TSQL
- syslogins
- sys.syslogins
- sys.syslogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syslogins compatibility view
- syslogins system table
ms.assetid: 4cb34f17-a4bb-469f-a218-71f074e6308f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54372511cab4cbcc3ecd7d2afe875325e105163d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62671927"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個登入帳戶，各包含一個資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至[目前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**sid**|**varbinary(85)**|安全性識別碼。|  
|**status**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**createdate**|**datetime**|加入登入的日期。|  
|**updatedate**|**datetime**|更新登入的日期。|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**name**|**sysname**|使用者的登入名稱。|  
|**dbname**|**sysname**|當建立連接時，使用者的預設資料庫名稱。|  
|**password**|**nvarchar(128)**|傳回 NULL。|  
|**language**|**sysname**|使用者的預設名稱。|  
|**denylogin**|**int**|1 = 登入是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者或群組，已被拒絕存取。|  
|**hasaccess**|**int**|1 = 登入已被授與伺服器的存取權。|  
|**isntname**|**int**|1 = 登入是 Windows 使用者或群組。<br /><br /> 0 = 登入為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。|  
|**isntgroup**|**int**|1 = 登入是 Windows 群組。|  
|**isntuser**|**int**|1 = 登入是 Windows 使用者。|  
|**sysadmin**|**int**|1 = 登入是隸屬**sysadmin**伺服器角色。|  
|**securityadmin**|**int**|1 = 登入是隸屬**securityadmin**伺服器角色。|  
|**serveradmin**|**int**|1 = 登入是隸屬**serveradmin**固定的伺服器角色。|  
|**setupadmin**|**int**|1 = 登入是隸屬**setupadmin**固定的伺服器角色。|  
|**processadmin**|**int**|1 = 登入是隸屬**processadmin**固定的伺服器角色。|  
|**diskadmin**|**int**|1 = 登入是隸屬**diskadmin**固定的伺服器角色。|  
|**dbcreator**|**int**|1 = 登入是隸屬**dbcreator**固定的伺服器角色。|  
|**bulkadmin**|**int**|1 = 登入是隸屬**bulkadmin**固定的伺服器角色。|  
|**loginname**|**nvarchar(128)**|使用者的登入名稱。 提供這個項目的目的，是為了與舊版相容。|  
  
## <a name="see-also"></a>另請參閱  
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [相容性檢視 &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
