---
title: sys.user_token (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.user_token
- user_token
- sys.user_token_TSQL
- user_token_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], security tokens
- sys.user_token catalog view
- user tokens [SQL Server]
- tokens [SQL Server]
- user_token catalog view
ms.assetid: be018103-5e57-43a4-9160-9bf420892aa7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a120fe3802235ff0d5548693d9bf7f4638ef5e42
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "59506485"
---
# <a name="sysusertoken-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用者 Token 一部分的每一個資料庫主體，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|主體的識別碼。 該值在資料庫中是唯一的。|  
|**sid**|**varbinary(85)**|如果主體是定義在資料庫外部，則為該主體的安全性識別碼。 例如，它可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入、Windows 登入、Windows 群組登入或是對應到憑證的登入，否則這個值為 NULL。|  
|**name**|**nvarchar (128)**|主體的名稱。 該值在資料庫中是唯一的。|  
|**type**|**nvarchar (128)**|主體類型的描述。 所有的類型會對應至**sid**。 這個值可以是下列值之一：<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**usage**|**nvarchar (128)**|指出主體參與了 GRANT 或 DENY 權限的評估，或者作為驗證器使用。<br /><br /> 這個值可以是下列其中一個值：<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>另請參閱  
 [sys.login_token &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
