---
description: DENY 物件權限 (Transact-SQL)
title: DENY 物件權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, objects
- table permissions [SQL Server]
ms.assetid: 0b8d3ddc-38c0-4241-b7bb-ee654a5081aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fae275453fd14afacc700150c93cc6a091141a11
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688617"
---
# <a name="deny-object-permissions-transact-sql"></a>DENY 物件權限 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  為安全性實體之 OBJECT 類別的成員定義權限。 OBJECT 類別的成員包括：資料表、檢視表、資料表值函式、預存程序、擴充預存程序、純量函數、彙總函式、服務佇列和同義字。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DENY <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        TO <database_principal> [ ,...n ]   
    [ CASCADE ]  
        [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *permission*  
 指定可以拒絕的結構描述所含物件之權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ALL  
 拒絕 ALL 不會拒絕所有可能的權限。 拒絕 ALL 相當於拒絕所有適用於指定物件的 ANSI-92 權限。 ALL 有多種意義，如下所示：  
  
 - 純量函式權限：EXECUTE、REFERENCES。  
 - 資料表值函式權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
 - 預存程序權限：EXECUTE。  
 - 資料表權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
 - 檢視權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
PRIVILEGES  
 為符合 ANSI-92 而包含這個項目。 不會變更 ALL 的行為。  
  
*column*  
 在拒絕其權限之資料表、檢視或資料表值函式中指定資料行名稱。 它必須以括弧 **( )** 括住。 只能拒絕資料行的 SELECT、REFERENCES 及 UPDATE 權限。 *column* 可以在權限子句中或在安全性實體名稱之後指定 。  
  
> [!CAUTION]  
>  資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。  
  
 ON [ OBJECT **::** ] [ *schema_name* ] **.** *object_name*  
 指定要拒絕其權限的物件。 若指定 *schema_name*，則 OBJECT 片語為選擇性。 若使用 OBJECT 片語，則範圍限定詞 ( **::** ) 為必要項目。 若未指定 *schema_name*，則會使用預設結構描述。 如果指定 *schema_name*，則結構描述範圍限定詞 ( **.** ) 為必要項目。  
  
 TO \<database_principal>  
 指定要拒絕其權限的主體。  
  
 CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
 AS \<database_principal>  
 指定主體，執行這項查詢的主體會從這個主體衍生權限來拒絕權限。  
  
 *Database_user*  
 指定資料庫使用者。  
  
 *Database_role*  
 指定資料庫角色。  
  
 *Application_role*  
 指定應用程式角色。  
  
 *Database_user_mapped_to_Windows_User*  
 指定對應至 Windows 使用者的資料庫使用者。  
  
 *Database_user_mapped_to_Windows_Group*  
 指定對應至 Windows 群組的資料庫使用者。  
  
 *Database_user_mapped_to_certificate*  
 指定對應至憑證的資料庫使用者。  
  
 *Database_user_mapped_to_asymmetric_key*  
 指定對應至非對稱金鑰的資料庫使用者。  
  
 *Database_user_with_no_login*  
 指定不含對應伺服器層級主體的資料庫使用者。  
  
## <a name="remarks"></a>備註  
 可以在各種目錄檢視中看到物件的相關資訊。 如需詳細資訊，請參閱[物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)。  
  
 物件是一個由結構描述所包含的結構描述層級安全性實體，在權限階層中，此結構描述為該安全性實體的父系。 下表所列的是可以拒絕之最特定和最有限制的物件權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|物件權限|物件權限所隱含|結構描述權限所隱含|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|刪除|CONTROL|刪除|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|執行 CREATE 陳述式之前，請先執行|  
|Insert|CONTROL|Insert|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>權限  
 需要物件的 CONTROL 權限。  
  
 如果是使用 AS 子句，指定的主體必須擁有要拒絕其權限的物件。  
  
## <a name="examples"></a>範例  
下列範例使用 AdventureWorks 資料庫。
  
### <a name="a-denying-select-permission-on-a-table"></a>A. 拒絕資料表的 SELECT 權限  
 下列範例會拒絕使用者 `RosaQdM` 對 `Person.Address` 資料表的 `SELECT` 權限。  
  
```sql  
DENY SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-denying-execute-permission-on-a-stored-procedure"></a>B. 拒絕預存程序的 EXECUTE 權限  
 下列範例會對一個稱為 `EXECUTE` 的應用程式角色拒絕預存程序 `HumanResources.uspUpdateEmployeeHireInfo` 的 `Recruiting11` 權限。  
  
```sql  
DENY EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-denying-references-permission-on-a-view-with-cascade"></a>C. 拒絕具有 CASCADE 之檢視的 REFERENCES 權限  
 下列範例會對具有 `REFERENCES` 之使用者 `BusinessEntityID` 拒絕檢視 `HumanResources.vEmployee` 中之資料行 `Wanida` 的 `CASCADE` 權限。  
  
```sql  
DENY REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  
