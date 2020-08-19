---
description: sys.user_token (Transact-SQL)
title: sys. user_token (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
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
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions|| = azure-sqldw-latest
ms.openlocfilehash: e8228ea67864645737524f9d449abb18fd1c1c6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419942"
---
# <a name="sysuser_token-transact-sql"></a>sys.user_token (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  針對屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用者 Token 一部分的每一個資料庫主體，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**principal_id**|**int**|主體的識別碼。 該值在資料庫中是唯一的。|  
|**希**|**Varbinary (85) **|如果主體是定義在資料庫外部，則為該主體的安全性識別碼。 例如，它可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入、Windows 登入、Windows 群組登入或是對應到憑證的登入，否則這個值為 NULL。|  
|**name**|**nvarchar (128)**|主體的名稱。 該值在資料庫中是唯一的。|  
|**type**|**nvarchar (128)**|主體類型的描述。 所有類型都會對應至 **sid**。 這個值可以是下列值之一：<br /><br /> SQL USER<br /><br /> WINDOWS LOGIN<br /><br /> WINDOWS GROUP<br /><br /> ROLE<br /><br /> APPLICATION ROLE<br /><br /> DATABASE ROLE<br /><br /> USER MAPPED TO CERTIFICATE<br /><br /> USER MAPPED TO ASYMMETRIC KEY<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC KEY|  
|**使用**|**nvarchar (128)**|指出主體參與了 GRANT 或 DENY 權限的評估，或者作為驗證器使用。<br /><br /> 這個值可以是下列其中一個值：<br /><br /> GRANT OR DENY<br /><br /> DENY ONLY<br /><br /> AUTHENTICATOR|  
  
## <a name="see-also"></a>另請參閱  
 [sys. login_token &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
