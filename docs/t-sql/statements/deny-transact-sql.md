---
title: DENY (Transact-SQL)
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DENY
- DENY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- security [SQL Server], denying access
- DENY statement
- permissions [SQL Server], denying
- server-level securables [SQL Server]
- inherited security settings [SQL Server]
- denying permissions [SQL Server], DENY statement
- principal security [SQL Server]
- database-level securables [SQL Server]
- denying permissions [SQL Server]
ms.assetid: c32d1e01-9ee9-4665-a516-fcfece58078e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e146021bf3bd601e01f6220ffcf42de970e63657
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484816"
---
# <a name="deny-transact-sql"></a>DENY (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  對主體拒絕權限。 防止主體透過其群組或角色成員資格繼承權限。 DENY 的優先順序高於所有權限，不同之處在於 DENY 不適用至物件擁有者或 sysadmin 固定伺服器角色的成員。
  **安全性注意事項**：系統無法拒絕 sysadmin 固定伺服器角色和物件擁有者的權限。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for DENY  
DENY   { ALL [ PRIVILEGES ] } 
     | <permission>  [ ( column [ ,...n ] ) ] [ ,...n ]  
    [ ON [ <class> :: ] securable ] 
    TO principal [ ,...n ]   
    [ CASCADE] [ AS principal ]  
[;]

<permission> ::=  
{ see the tables below }  
  
<class> ::=  
{ see the tables below }  
```  
  
```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
<permission> ::=  
{ see the tables below }  
  
<class> ::=  
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
 這個選項不會拒絕所有可能的權限。 拒絕 ALL 等同於拒絕下列權限。  
  
-   如果安全性實體是資料庫，ALL 表示 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
-   如果安全性實體是純量函數，ALL 表示 EXECUTE 和 REFERENCES。  
  
-   如果安全性實體是資料表值函式，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是預存程序，ALL 表示 EXECUTE。  
  
-   如果安全性實體是資料表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是檢視表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
> [!NOTE]  
>  DENY ALL 語法已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 改為拒絕特定的權限。  
  
 PRIVILEGES  
 為符合 ISO 而包含這個項目。 不會變更 ALL 的行為。  
  
 *permission*  
 這是權限的名稱。 權限對安全性實體的有效對應描述於下列子主題中。  
  
 *column*  
 指定正在拒絕權限的資料表中資料行的名稱。 它必須用括號 () 括住。  
  
 *class*  
 指定正在拒絕權限之安全性實體的類別。 範圍限定詞 **::** 為必要項目。  
  
 *securable*  
 指定正在拒絕權限的安全性實體。  
  
 TO *principal*  
 這是主體的名稱。 可以被拒絕安全性實體權限的主體，隨著安全性實體而不同。 如需有效的組合，請參閱下列安全性實體特定主題。  
  
 CASCADE  
 表示已對指定主體和對被主體授與權限的所有其他主體拒絕權限。 當主體具有 GRANT OPTION 的權限時，這是必要的。  
  
 AS *principal*  
 指定主體，執行這項查詢的主體會從這個主體衍生權限來拒絕權限。
您可使用 AS principal 子句，來表示記錄為權限拒絕者的主體應為陳述式執行人員以外的主體。 例如，假設使用者 Mary 是 principal_id 12；使用者 Raul 是 principal 15。 Mary 執行 `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`。現在，即使實際執行陳述式的是使用者 13 (Mary)，sys.database_permissions 資料表仍會指出 deny 陳述式的 grantor_prinicpal_id 是 15 (Raul)。
  
在此陳述式中使用 AS 不代表能模擬其他使用者。  
  
## <a name="remarks"></a>備註  
 DENY 陳述式的完整語法相當複雜。 上方的語法圖已簡化，以強調其結構。 拒絕特定安全性實體權限的完整語法描述於下列主題中。  
  
 如果針對被授與指定 GRANT OPTION 之權限的主體拒絕權限時，並沒有指定 CASCADE，DENY 便會失敗。  
  
 sp_helprotect 系統預存程序會報告資料庫層級安全性實體的權限。  
  
> [!CAUTION]  
>  資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。 未來的版本將予以移除。  
  
> [!CAUTION]  
>  拒絕資料庫的 CONTROL 權限隱含著拒絕資料庫的 CONNECT 權限。 被拒絕資料庫 CONTROL 權限的主體將無法連接至該資料庫。  
  
> [!CAUTION]  
>  拒絕 CONTROL SERVER 權限隱含著拒絕伺服器的 CONNECT SQL 權限。 被拒絕伺服器 CONTROL SERVER 權限的主體將無法連接至該伺服器。  
  
## <a name="permissions"></a>權限  
 呼叫端 (或指定了 AS 選項的主體) 必須具有安全性實體的 CONTROL 權限，或是具有隱含安全性實體 CONTROL 權限的更高權限。 如果使用 AS 選項，指定的主體必須擁有要拒絕其權限的類型。  
  
 CONTROL SERVER 權限的被授與者 (例如系統管理員 (sysadmin) 固定伺服器角色的成員)，可以拒絕伺服器中任何安全性實體的任何權限。 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以拒絕資料庫中任何安全性實體的任何權限。 結構描述之 CONTROL 權限的被授與者，可以拒絕結構描述中任何物件的任何權限。 如果使用 AS 子句，指定的主體必須擁有要拒絕其權限的類型。  
  
## <a name="examples"></a>範例

 下表列出安全性實體和描述安全性實體特定語法的主題。  
  
|安全性實體|語法|
|----------|------|
|應用程式角色|[DENY 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|組件|[DENY 組件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-assembly-permissions-transact-sql.md)|  
|非對稱金鑰|[DENY 非對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-asymmetric-key-permissions-transact-sql.md)|  
|可用性群組|[DENY 可用性群組權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)|  
|憑證|[DENY 憑證權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-certificate-permissions-transact-sql.md)|  
|合約|[DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|資料庫|[DENY 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-permissions-transact-sql.md)|  
|資料庫範圍認證|[DENY 資料庫範圍認證 (TRANSACT-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)|  
|端點|[DENY 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)|  
|全文檢索目錄|[DENY 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|全文檢索停用字詞表|[DENY 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-full-text-permissions-transact-sql.md)|  
|函式|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|登入|[DENY 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)|  
|訊息類型|[DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|Object|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|佇列|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|遠端服務繫結|[DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|角色|[DENY 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|路由|[DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|結構描述|[DENY 結構描述權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-schema-permissions-transact-sql.md)|  
|搜尋屬性清單|[DENY 搜尋屬性清單權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-search-property-list-permissions-transact-sql.md)|  
|伺服器|[DENY 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)|  
|服務|[DENY Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-service-broker-permissions-transact-sql.md)|  
|預存程序|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|對稱金鑰|[DENY 對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)|  
|同義字|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|系統物件|[DENY 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)|  
|Table|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|類型|[DENY 類型權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)|  
|User|[DENY 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)|  
|檢視|[DENY 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)|  
|XML 結構描述集合|[DENY XML 結構描述集合權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
