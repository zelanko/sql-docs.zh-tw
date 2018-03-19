---
title: "DENY 資料庫範圍認證 (TRANSACT-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DENY DATABASE SCOPED CREDENTIAL
- DENY_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, database scoped credentials
- denying permissions [SQL Server], database scoped credential
ms.assetid: c508b1c9-169e-4e7a-9a49-7ddf2ca8f848
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: adcbe36f2ffabfc63521fe905933295402178977
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="deny-database-scoped-credential-transact-sql"></a>DENY 資料庫範圍認證 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  拒絕資料庫範圍認證的權限。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DENY permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ]  
    [ CASCADE ]  
    [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>引數  
 *permission*  
 指定可在資料庫範圍認證拒絕的權限。 如下所列。  
  
 ON DATABASE SCOPED CREDENTIAL **::***credential_name*  
 指定拒絕權限的資料庫範圍認證。 需要範圍限定詞 "::"。  
  
 *database_principal*  
 指定要拒絕其權限的主體。 它有下列幾種：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
 CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
 *denying_principal*  
 指定主體，執行這項查詢的主體會從這個主體衍生權限來拒絕權限。 它有下列幾種：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
## <a name="remarks"></a>Remarks  
 資料庫範圍認證是包含在資料庫內的資料庫層級安全性實體，在權限階層中，該資料庫為其父系。 下方列出用資料庫範圍認證可拒絕的最特定也最有限權限，另外還有以隱含方式加以涵蓋的較通用權限。  
  
|資料庫範圍認證權限|資料庫範圍認證權限所隱含|資料庫權限所隱含|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要資料庫範圍認證的 CONTROL 權限。 如果使用 AS 子句，指定的主體必須擁有資料庫範圍認證。  
  
## <a name="see-also"></a>另請參閱  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [REVOKE 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
