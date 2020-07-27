---
title: GRANT (Transact-SQL)
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b89b170d50e23c14cf08da78597e83c674050de0
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86483794"
---
# <a name="grant-transact-sql"></a>GRANT (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  將安全性實體的權限授與某個主體。  一般概念是 GRANT \<some permission> ON \<some object> TO \<some user, login, or group>。 如需權限的一般說明，請參閱[權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "文章連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for GRANT  
GRANT { ALL [ PRIVILEGES ] }  
      | permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      [ ON [ class :: ] securable ] TO principal [ ,...n ]   
      [ WITH GRANT OPTION ] [ AS principal ]  
```  
  
```syntaxsql
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數

ALL  
這個選項已被取代，只保留回溯相容性。 它不會授與所有可能的權限。 授與 ALL 等同於授與下列權限：

  - 如果安全性實體是資料庫，ALL 表示 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
  - 如果安全性實體是純量函數，ALL 表示 EXECUTE 和 REFERENCES。  
  
  - 如果安全性實體是資料表值函式，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
  - 如果安全性實體是預存程序，ALL 表示 EXECUTE。  
  
  - 如果安全性實體是資料表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
  - 如果安全性實體是檢視表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  

PRIVILEGES  
為符合 ISO 而包含這個項目。 不會變更 ALL 的行為。  
  
*permission*  
這是權限的名稱。 下列子主題描述權限與安全性實體的有效對應。  
  
*column*  
指定正在授與權限的資料表中資料行的名稱。 它必須用括號 () 括住。  
  
*class*  
指定正在授與權限之安全性實體的類別。 範圍限定詞 **::** 為必要項目。  
  
*securable*  
指定要授與其權限的安全性實體。  
  
TO *principal*  
這是主體的名稱。 可以被授與安全性實體權限的主體，隨著安全性實體而不同。 如需有效的組合，請參閱下列子主題。  
  
GRANT OPTION  
指出也會提供被授與者授與指定權限給其他主體的能力。  
  
AS *principal*  
您可使用 AS principal 子句，來表示記錄為權限授與者的主體應為陳述式執行人員以外的主體。 例如，假設使用者 Mary 是 principal_id 12；使用者 Raul 是 principal 15。 Mary 執行 `GRANT SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`。現在，即使實際執行陳述式的是使用者 13 (Mary)，sys。 .database_permissions 資料表仍會指出 grantor_prinicpal_id 是 15 (Raul)。  

通常不建議使用 AS 子句，除非您需要明確定義權限鏈結。 如需詳細資訊，請參閱[權限 (資料庫引擎)](../../relational-databases/security/permissions-database-engine.md) 的**權限檢查演算法的摘要**一節。

在此陳述式中使用 AS 不代表能模擬其他使用者。

## <a name="remarks"></a>備註

GRANT 陳述式的完整語法相當複雜。 上方的語法圖已簡化，以強調其結構。 下列文章描述授與特定安全性實體權限的完整語法。  

REVOKE 陳述式可用來移除授與的權限，而 DENY 陳述式可用來避免主體透過 GRANT 取得特定權限。  

授與權限會移除指定安全性實體權限的 DENY 或 REVOKE。 如果相同權限在包含安全性實體的更高範圍被拒絕，則 DENY 的優先順序較高。 但是在更高範圍撤銷授與權限的優先順序並不會比較高。  

資料庫層級權限是在指定資料庫的範圍內授與。 如果使用者必須具有其他資料庫中的物件權限，應在其他資料庫中建立使用者帳戶，或將使用者帳戶存取權授與其他資料庫和目前的資料庫。  

> [!CAUTION]  
> 資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。 未來的版本將予以移除。  

sp_helprotect 系統預存程序會報告資料庫層級安全性實體的權限。  

## <a name="with-grant-option"></a>WITH GRANT OPTION

**GRANT** ...**WITH GRANT OPTION** 會指定接收權限的安全性主體能夠將指定的權限授與其他安全性帳戶。 當接收權限的主體是角色或 Windows 群組時，如果物件權限需要進一步授與非群組或角色成員的使用者，就必須使用 **AS** 子句。 因為只有使用者 (而非群組或角色) 能夠執行 **GRANT** 陳述式，所以群組或角色的特定成員必須在授與權限時使用 **AS** 子句來明確叫用角色或群組成員資格。 下列範例顯示如何在授權給角色或 Windows 群組時使用 **WITH GRANT OPTION**。  
  
```sql
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

如需所有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 權限的 PDF 格式海報大小圖表，請參閱 [https://aka.ms/sql-permissions-poster](https://aka.ms/sql-permissions-poster)。  

## <a name="permissions"></a>權限

同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。 如果是使用 AS 選項，就必須套用額外的需求。 如需詳細資料，請參閱安全性實體的特定文章。

物件擁有者可以授與他們所擁有之物件的權限。 具有安全性實體之 CONTROL 權限的主體可以授與該安全性實體的權限。

CONTROL SERVER 權限的被授與者 (例如系統管理員 (sysadmin) 固定伺服器角色的成員)，可以授與伺服器中任何安全性實體的任何權限。 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以授予資料庫中任何安全性實體的任何權限。 結構描述之 CONTROL 權限的被授與者，可以授與結構描述中任何物件的任何權限。

## <a name="examples"></a>範例

下表列出安全性實體和描述安全性實體特定語法的文章。  

| 安全性實體 | GRANT 語法|
| ---------| ------ |
|應用程式角色|[GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|組件|[GRANT 組件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-assembly-permissions-transact-sql.md)|  
|非對稱金鑰|[GRANT 非對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-asymmetric-key-permissions-transact-sql.md)|  
|可用性群組|[GRANT 可用性群組權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)|  
|憑證|[GRANT 憑證權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-certificate-permissions-transact-sql.md)|  
|合約|[GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|資料庫|[GRANT 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)|
|資料庫範圍認證|[GRANT 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)|  
|端點|[GRANT 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)|  
|全文檢索目錄|[GRANT 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|全文檢索停用字詞表|[GRANT 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-full-text-permissions-transact-sql.md)|  
|函式|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|登入|[GRANT 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)|  
|訊息類型|[GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|Object|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|佇列|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|遠端服務繫結|[GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|角色|[GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|路由|[GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|結構描述|[GRANT 結構描述權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-schema-permissions-transact-sql.md)|  
|搜尋屬性清單|[GRANT 搜尋屬性清單權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-search-property-list-permissions-transact-sql.md)|  
|伺服器|[GRANT 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)|  
|服務|[GRANT Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-service-broker-permissions-transact-sql.md)|  
|預存程序|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|對稱金鑰|[GRANT 對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)|  
|同義字|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|系統物件|[GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)|  
|Table|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|類型|[GRANT 類型權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)|  
|User|[GRANT 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)|  
|檢視|[GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)|  
|XML 結構描述集合|[GRANT XML 結構描述集合權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-xml-schema-collection-permissions-transact-sql.md)|  

## <a name="see-also"></a>另請參閱

- [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)
- [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)
- [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)
- [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)
- [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)
- [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)
- [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)
- [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)