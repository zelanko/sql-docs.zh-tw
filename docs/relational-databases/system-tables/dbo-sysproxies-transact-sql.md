---
title: dbo. sysproxies （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 1dd486757a912d8f0364f55570a368292cf39ab7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67984901"
---
# <a name="dbosysproxies-transact-sql"></a>dbo.sysproxies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶的屬性。 此資料表會儲存在**msdb**資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 帳戶的識別碼。|  
|**name**|**sysname**|Proxy 帳戶的名稱。|  
|**credential_id**|**int**|Proxy 帳戶使用的認證識別碼。|  
|**後**|**tinyint**|Proxy 帳戶的狀態：<br /><br /> **0** = 已停用。 **1** = 已啟用。|  
|**描述**|**nvarchar(512)**|當建立 Proxy 帳戶時，使用者所輸入的描述。|  
|**user_sid**|**Varbinary （85）**|與 proxy 認證相關聯之使用者或群組的 Microsoft Windows *security_identifier* 。|  
|**credential_date_created**|**datetime**|認證的建立日期和時間。|  
  
## <a name="remarks"></a>備註  
 只有**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠存取**sysproxies**資料表。  
  
## <a name="see-also"></a>另請參閱  
 [sysproxylogin &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxylogin-transact-sql.md)   
 [sysproxysubsystem &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [syssubsystems &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-syssubsystems-transact-sql.md)  
  
  
