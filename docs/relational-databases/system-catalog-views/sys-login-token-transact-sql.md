---
description: sys.login_token (Transact-SQL)
title: sys. login_token (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- login_token_TSQL
- sys.login_token_TSQL
- sys.login_token
- login_token
dev_langs:
- TSQL
helpviewer_keywords:
- sys.login_token catalog view
- logins [SQL Server], security tokens
- tokens [SQL Server]
ms.assetid: 86e06938-9d0a-44e5-99e2-55c8ef5f2f84
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 339964a859d5e95d88853781a8b2b43f341f23be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377804"
---
# <a name="syslogin_token-transact-sql"></a>sys.login_token (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對屬於登入 Token 一部分的每個伺服器主體，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|主體的識別碼。 這個值在伺服器中是唯一的。|  
|**希**|**Varbinary (85) **|主體的安全性識別碼。 如果這是 Windows 主體， **sid** = windows sid。 如果登入對應至憑證，則 **sid** = 來自憑證的 GUID。|  
|**name**|**nvarchar(128)**|主體的名稱。 這個值在伺服器中是唯一的。|  
|**type**|**nvarchar(128)**|主體類型的描述。 所有類型都會對應至 **sid**。 這個值可以是下列值之一：<br /><br /> SQL LOGIN<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> SERVER ROLE<br /><br /> LOGIN MAPPED TO CERTIFICATE<br /><br /> LOGIN MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**使用**|**nvarchar(128)**|指出主體參與了 GRANT 或 DENY 權限的評估，或者作為驗證器使用。<br /><br /> 這個值可以是下列其中一個值：<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>另請參閱  
 [sys. user_token &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
