---
title: "GRANT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GRANT_TSQL
- GRANT
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], GRANT statement
- schema-level securables [SQL Server]
- GRANT statement
- cross-database permissions
- GRANT statement, about GRANT statement
- server-level securables [SQL Server]
- database-level securables [SQL Server]
- permissions [SQL Server], granting
ms.assetid: a760c16a-4d2d-43f2-be81-ae9315f38185
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bb9bf548f042a4a6f41322fb789a2cd7e5b6bec9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將安全性實體的權限授與某個主體。  一般概念是 GRANT\<某些權限 > ON\<某個物件 > TO\<某些使用者、 登入或群組 >。 如需權限的一般討論，請參閱[權限 &#40; Database engine&#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class_type> ::=  
{  
      LOGIN  
    | DATABASE  
    | OBJECT  
    | ROLE  
    | SCHEMA  
    | USER  
}  
```  
  
## <a name="arguments"></a>引數  
 ALL  
 這個選項已被取代，只保留回溯相容性。 它不會授與所有可能的權限。 授與 ALL 等同於授與下列權限。  
  
-   如果安全性實體是資料庫，ALL 表示 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
-   如果安全性實體是純量函數，ALL 表示 EXECUTE 和 REFERENCES。  
  
-   如果安全性實體是資料表值函式，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是預存程序，ALL 表示 EXECUTE。  
  
-   如果安全性實體是資料表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是檢視表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
PRIVILEGES  
 為符合 ISO 而包含這個項目。 不會變更 ALL 的行為。  
  
*權限*  
 這是權限的名稱。 權限對安全性實體的有效對應描述於下列子主題中。  
  
*資料行*  
 指定正在授與權限的資料表中資料行的名稱。 它必須用括號 () 括住。  
  
*類別*  
 指定正在授與權限之安全性實體的類別。 範圍限定詞**::**需要。  
  
*安全性實體*  
 指定要授與其權限的安全性實體。  
  
若要*主體*  
 這是主體的名稱。 可以被授與安全性實體權限的主體，隨著安全性實體而不同。 如需有效的組合，請參閱下列子主題。  
  
GRANT OPTION  
 指出也會提供被授與者授與指定權限給其他主體的能力。  
  
AS*主體*  
 使用 AS 主體子句來表示 主體記錄為權限授與者應該是執行陳述式的人員以外的主體。 例如，假設使用者 Mary 是 principal_id 12，和使用者阿為主體 15。 Mary 執行`GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`現在 sys.database_permissions 資料表會指出 grantor_prinicpal_id 已 15 （阿），即使使用者 13 (Mary) 實際執行的陳述式。

通常不建議使用 AS 子句，除非您需要明確定義的權限鏈結。 如需詳細資訊，請參閱**權限檢查演算法的摘要**區段[權限 (Database Engine)](../../relational-databases/security/permissions-database-engine.md)。

使用此陳述式與不表示模擬另一位使用者的能力。 
  
## <a name="remarks"></a>備註  
 GRANT 陳述式的完整語法相當複雜。 上方的語法圖已簡化，以強調其結構。 授與特定安全性實體權限的完整語法描述於下列主題中。  
  
 REVOKE 陳述式可用來移除授與的權限，而 DENY 陳述式可用來避免主體透過 GRANT 取得特定權限。  
  
 授與權限會移除指定安全性實體權限的 DENY 或 REVOKE。 如果相同權限在包含安全性實體的更高範圍被拒絕，則 DENY 的優先順序較高。 但是在更高範圍撤銷授與權限的優先順序並不會比較高。  
  
 資料庫層級權限是在指定資料庫的範圍內授與。 如果使用者必須具有其他資料庫中的物件權限，應在其他資料庫中建立使用者帳戶，或將使用者帳戶存取權授與其他資料庫和目前的資料庫。  
  
> [!CAUTION]  
>  資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。 未來的版本將予以移除。  
  
 sp_helprotect 系統預存程序會報告資料庫層級安全性實體的權限。  
  
## <a name="with-grant-option"></a>WITH GRANT OPTION  
 **GRANT** ... **具有 GRANT OPTION**指定接收權限的安全性主體有授與其他安全性帳戶所指定權限的能力。 當接收權限的主體是角色或 Windows 群組**AS**的物件權限需要進一步授與使用者群組或角色的成員時，就必須使用子句。 因為只有使用者，而不是群組或角色，可以執行**GRANT**陳述式中，特定群組或角色的成員必須使用**AS**子句來明確叫用的角色或群組的成員資格授與時權限。 下列範例會示範如何**WITH GRANT OPTION**授與角色或 Windows 群組時，會使用。  
  
```  
-- Execute the following as a database owner  
GRANT EXECUTE ON TestProc TO TesterRole WITH GRANT OPTION;  
EXEC sp_addrolemember TesterRole, User1;  
-- Execute the following as User1  
-- The following fails because User1 does not have the permission as the User1  
GRANT EXECUTE ON TestMe TO User2;  
-- The following succeeds because User1 invokes the TesterRole membership  
GRANT EXECUTE ON TestMe TO User2 AS TesterRole;  
```  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 權限的圖表  
 如需 PDF 格式之海報大小的所有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 權限圖表，請參閱 [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="permissions"></a>Permissions  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。 如果是使用 AS 選項，就必須套用額外的需求。 如需詳細資料，請參閱安全性實體特定主題。  
  
 物件擁有者可以授與他們所擁有之物件的權限。 具有安全性實體之 CONTROL 權限的主體可以授與該安全性實體的權限。  
  
 CONTROL SERVER 權限的被授與者 (例如系統管理員 (sysadmin) 固定伺服器角色的成員)，可以授與伺服器中任何安全性實體的任何權限。 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以授予資料庫中任何安全性實體的任何權限。 結構描述之 CONTROL 權限的被授與者，可以授與結構描述中任何物件的任何權限。  
  
## <a name="examples"></a>範例  
 下表列出安全性實體和描述安全性實體特定語法的主題。  
  
|||  
|-|-|  
|應用程式角色|[GRANT 資料庫主體權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|組件|[授與組件的權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|非對稱金鑰|[授與非對稱金鑰權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|可用性群組|[授與可用性群組的權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|憑證|[GRANT 憑證權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|合約|[授與 Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|資料庫|[GRANT 資料庫權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|資料庫範圍認證|[授與資料庫範圍認證 (TRANSACT-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|端點|[GRANT 端點權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|全文檢索目錄|[授與全文檢索權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|全文檢索停用字詞表|[授與全文檢索權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|函數|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|登入|[GRANT 伺服器主體權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|訊息類型|[授與 Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|物件|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|佇列|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|遠端服務繫結|[授與 Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|角色|[GRANT 資料庫主體權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|路由|[授與 Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|結構描述|[授與結構描述權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|搜尋屬性清單|[GRANT 搜尋屬性清單權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|Server|[GRANT 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|服務|[授與 Service Broker 權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|預存程序|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|對稱金鑰|[授與對稱金鑰權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|同義字|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|系統物件|[GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Table|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|類型|[GRANT 類型權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|使用者|[GRANT 資料庫主體權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|檢視|[GRANT 物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML 結構描述集合|[授與 XML 結構描述集合權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  

