---
title: dbo.sysproxies (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysproxies_TSQL
- sysproxies_TSQL
- dbo.sysproxies
- sysproxies
dev_langs:
- TSQL
helpviewer_keywords:
- sysproxies system table
ms.assetid: a73da875-be22-45fc-b5e2-ea7ebd48e2d6
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb17d288b1ca85adad9c686b550bfcdf68c90b73
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的屬性。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。|  
|**name**|**sysname**|Proxy 帳戶的名稱。|  
|**credential_id**|**int**|Proxy 帳戶使用的認證識別碼。|  
|**enabled**|**tinyint**|Proxy 帳戶的狀態：<br /><br /> **0** = 已停用。 **1** = 啟用。|  
|**描述**|**nvarchar(512)**|當建立 Proxy 帳戶時，使用者所輸入的描述。|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier*的使用者或群組相關聯的 proxy 認證。|  
|**credential_date_created**|**datetime**|認證的建立日期和時間。|  
  
## <a name="remarks"></a>備註  
 只有成員**sysadmin**固定的伺服器角色可以存取**sysproxies**資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysproxylogin &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
