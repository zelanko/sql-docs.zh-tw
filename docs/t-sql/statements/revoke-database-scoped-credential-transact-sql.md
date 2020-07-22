---
title: REVOKE 資料庫範圍認證 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- REVOKE DATABASE SCOPED CREDENTIAL
- REVOKE_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statements, database scoped credentials
- revoking permissions [SQL Server], database scoped credentials
ms.assetid: b73233c5-9afa-48ca-ba34-a9f86b9b1d2e
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0469f4f03430433135c827bb8f6e6fa9ed5dcc4a
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485119"
---
# <a name="revoke-database-scoped-credential-transact-sql"></a>REVOKE 資料庫範圍認證 (Transact-SQL)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  撤銷資料庫範圍認證的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 GRANT OPTION FOR  
 表示將撤銷授與指定權限的能力。 不會撤銷權限本身。  
  
> [!IMPORTANT]  
>  如果主體有不含 GRANT 選項的指定權限，則會撤銷權限本身。  
  
 *permission*  
 指定可以撤銷的資料庫範圍認證權限。 如下所列。  
  
 ON CERTIFICATE **::** _credential_name_  
 指定要撤銷的資料庫範圍認證權限。 需要範圍限定詞 "::"。  
  
 *database_principal*  
 指定要撤銷其權限的主體。 下列其中之一：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
 CASCADE  
 指出目前正在撤銷的權限，也會從它被這個主體所授與的其他主體一起撤銷。  
  
> [!CAUTION]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *revoking_principal*  
 指定主體，執行這項查詢的主體會從這個主體衍生其權限來撤銷權限。 下列其中之一：  
  
-   資料庫使用者  
  
-   資料庫角色  
  
-   應用程式角色  
  
-   對應至 Windows 登入的資料庫使用者  
  
-   對應至 Windows 群組的資料庫使用者  
  
-   對應至憑證的資料庫使用者  
  
-   對應至非對稱金鑰的資料庫使用者  
  
-   未對應至伺服器主體的資料庫使用者  
  
## <a name="remarks"></a>備註  
 資料庫範圍認證是包含在資料庫內的資料庫層級安全性實體，在權限階層中，該資料庫為其父系。 下方列出的資料庫範圍認證權限，是可以撤銷的最明確與最有限權限，以及隱含包括這些權限的一般權限。  
  
|資料庫範圍認證權限|資料庫範圍認證權限所隱含|資料庫權限所隱含|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>權限  
 需要資料庫範圍認證的 CONTROL 權限。  
  
## <a name="see-also"></a>另請參閱  
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)      
 [GRANT 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [DENY 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
