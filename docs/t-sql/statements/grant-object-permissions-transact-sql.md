---
title: GRANT 物件權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], objects
- GRANT statement, objects
ms.assetid: c001c2e7-d092-43d4-8fa6-693b3ec4c3ea
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed580cb28c65eab7f0abd7702cab623bcf9fcd2e
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54326319"
---
# <a name="grant-object-permissions-transact-sql"></a>GRANT 物件權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  授與資料表、檢視表、資料表值函式、預存程序、擴充預存程序、純量函數、彙總函式、服務佇列或同義字的權限。  
  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
    TO <database_principal> [ ,...n ]   
    [ WITH GRANT OPTION ]  
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
  
## <a name="arguments"></a>引數  
 *permission*  
 指定可授與的結構描述所含物件之權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ALL  
 授與 ALL 不會授與所有可能的權限。 授與 ALL 相當於授與適用於指定之物件的所有 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 權限。 ALL 有多種意義，如下所示：  
  
- 純量函數權限：EXECUTE、REFERENCES。  
- 資料表值函數權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
- 預存程序權限：EXECUTE。  
- 資料表權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
- 檢視表權限：DELETE、INSERT、REFERENCES、SELECT、UPDATE。  
  
PRIVILEGES  
 為符合 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]-92 而包含這個項目。 不會變更 ALL 的行為。  
  
*column*  
 在授與其權限之資料表、檢視或資料表值函式中指定資料行名稱。 必須以括弧 ( ) 括住。 只能授與資料行的 SELECT、REFERENCES 及 UPDATE 權限。 *column* 可以在權限子句中或在安全性實體名稱之後指定 。  
  
> [!CAUTION]  
>  資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。  
  
 ON [ OBJECT :: ] [ *schema_name* ] . *object_name*  
 指定正在授與權限的物件。 若指定 *schema_name*，則 OBJECT 片語為選擇性。 如果使用 OBJECT 片語，則需要範圍限定詞 (::)。 若未指定 *schema_name*，則會使用預設結構描述。 若指定 *schema_name*，則結構描述範圍限定詞 (.) 是必要項目。  
  
 TO \<database_principal>  
 指定要對其授與權限的主體。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS \<database_principal> 指定主體，以讓執行這項查詢的主體可從該主體衍生授與權限的權力。  
  
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
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  在某些情況下，ALTER 與 REFERENCE 權限的結合可允許被授與者檢視資料或執行未經授權的函數。 例如：擁有資料表的 ALTER 權限和函數的 REFERENCE 權限之使用者，可以透過函數來建立計算資料行並執行它。 在此情況下，使用者也需要計算資料行的 SELECT 權限。  
  
 可以在各種目錄檢視中看到物件的相關資訊。 如需詳細資訊，請參閱[物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)。  
  
 物件是一個由結構描述所包含的結構描述層級安全性實體，在權限階層中，此結構描述為該安全性實體的父系。 下表所列的是可以授與之最特定且最有限的物件權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|物件權限|物件權限所隱含|結構描述權限所隱含|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|Delete|CONTROL|Delete|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|執行 CREATE 陳述式之前，請先執行|  
|Insert|CONTROL|Insert|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>[權限]  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。  
  
 如果是使用 AS 選項，就必須套用下列其他需求。  
  
|AS|其他必要的權限|  
|--------|------------------------------------|  
|資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 登入的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至 Windows 群組的資料庫使用者|Windows 群組中的成員資格、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至憑證的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|對應至非對稱金鑰的資料庫使用者|db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|未對應至任何伺服器主體的資料庫使用者|使用者的 IMPERSONATE 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|資料庫角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
|應用程式角色|角色的 ALTER 權限、db_securityadmin 固定資料庫角色中的成員資格、db_owner 固定資料庫角色中的成員資格，或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-select-permission-on-a-table"></a>A. 授與資料表的 SELECT 權限  
 下列範例會將 `SELECT` 資料庫中之資料表 `RosaQdM` 的 `Person.Address` 權限，授與使用者 `AdventureWorks2012`。  
  
```  
GRANT SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-a-stored-procedure"></a>B. 授與預存程序的 EXECUTE 權限  
 下列範例會將預存程序 `EXECUTE` 的 `HumanResources.uspUpdateEmployeeHireInfo` 權限，授與一個稱為 `Recruiting11` 的應用程式角色。  
  
```  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-granting-references-permission-on-a-view-with-grant-option"></a>C. 授與具有 GRANT OPTION 之檢視的 REFERENCES 權限  
 下列範例會將檢視 `REFERENCES` 中之資料行 `BusinessEntityID` 的 `HumanResources.vEmployee` 權限，授與具有 `Wanida` 的使用者 `GRANT OPTION`。  
  
```  
GRANT REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida WITH GRANT OPTION;  
GO  
```  
  
### <a name="d-granting-select-permission-on-a-table-without-using-the-object-phrase"></a>D. 授與資料表的 SELECT 權限，但不使用 OBJECT 片語  
 下列範例會將 `SELECT` 資料庫中之資料表 `RosaQdM` 的 `Person.Address` 權限，授與使用者 `AdventureWorks2012`。  
  
```  
GRANT SELECT ON Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="e-granting-select-permission-on-a-table-to-a-domain-account"></a>E. 將資料表的 SELECT 權限授與網域帳戶  
 下列範例會將 `SELECT` 資料庫中之資料表 `AdventureWorks2012\RosaQdM` 的 `Person.Address` 權限，授與使用者 `AdventureWorks2012`。  
  
```  
GRANT SELECT ON Person.Address TO [AdventureWorks2012\RosaQdM];  
GO  
```  
  
### <a name="f-granting-execute-permission-on-a-procedure-to-a-role"></a>F. 將程序的 EXECUTE 權限授與角色  
 下列範例會建立一個角色，然後將 `EXECUTE` 資料庫中 `uspGetBillOfMaterials` 程序的 `AdventureWorks2012` 權限授與該角色。  
  
```  
CREATE ROLE newrole ;  
GRANT EXECUTE ON dbo.uspGetBillOfMaterials TO newrole ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

