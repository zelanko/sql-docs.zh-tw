---
title: dbo.sysproxies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a37300ad1bf16ac76fbcbd0c6e77870077f7f631
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846406"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的屬性。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。|  
|**name**|**sysname**|Proxy 帳戶的名稱。|  
|**credential_id**|**int**|Proxy 帳戶使用的認證識別碼。|  
|**enabled**|**tinyint**|Proxy 帳戶的狀態：<br /><br /> **0** = 已停用。 **1** = 啟用。|  
|**description**|**nvarchar(512)**|當建立 Proxy 帳戶時，使用者所輸入的描述。|  
|**user_sid**|**varbinary(85)**|Microsoft Windows *security_identifier&lt*的使用者或群組相關聯的 proxy 認證。|  
|**credential_date_created**|**datetime**|認證的建立日期和時間。|  
  
## <a name="remarks"></a>備註  
 只有成員**sysadmin**固定的伺服器角色可以存取**sysproxies**資料表。  
  
## <a name="see-also"></a>另請參閱  
 [dbo.sysproxylogin &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [dbo.sysproxysubsystem &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.syssubsystems &#40;Transact SQL&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
