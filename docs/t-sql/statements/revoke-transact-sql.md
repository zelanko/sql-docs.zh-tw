---
title: REVOKE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REVOKE_TSQL
- REVOKE
dev_langs:
- TSQL
helpviewer_keywords:
- schema-level securables [SQL Server]
- REVOKE statement, Transact-SQL syntax
- removing permissions
- server-level securables [SQL Server]
- deleting permissions
- revoking permissions [SQL Server]
- REVOKE statement
- denying permissions [SQL Server], removing
- database-level securables [SQL Server]
- granting permissions [SQL Server], removing
- permissions [SQL Server], revoking
- dropping permissions
ms.assetid: 9d31d3e7-0883-45cd-bf0e-f0361bbb0956
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c3f9ffc068b5729a257169fe4a65052d3d1c62ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67914204"
---
# <a name="revoke-transact-sql"></a>REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  移除先前授與或拒絕的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Simplified syntax for REVOKE  
REVOKE [ GRANT OPTION FOR ]  
      {   
        [ ALL [ PRIVILEGES ] ]  
        |  
                permission [ ( column [ ,...n ] ) ] [ ,...n ]  
      }  
      [ ON [ class :: ] securable ]   
      { TO | FROM } principal [ ,...n ]   
      [ CASCADE] [ AS principal ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
REVOKE   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    [ FROM | TO ] principal [ ,...n ]  
    [ CASCADE ]  
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
 GRANT OPTION FOR  
 表示將撤銷授與指定權限的能力。 這在您使用 CASCADE 引數時是必須的。  
  
> [!IMPORTANT]  
>  如果主體有不含 GRANT 選項的指定權限，則會撤銷權限本身。  
  
 ALL  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 這個選項不會撤銷所有可能的權限。 撤銷 ALL 等同於撤銷下列權限。  
  
-   如果安全性實體是資料庫，ALL 表示 BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
-   如果安全性實體是純量函數，ALL 表示 EXECUTE 和 REFERENCES。  
  
-   如果安全性實體是資料表值函式，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是預存程序，ALL 表示 EXECUTE。  
  
-   如果安全性實體是資料表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
-   如果安全性實體是檢視表，ALL 表示 DELETE、INSERT、REFERENCES、SELECT 和 UPDATE。  
  
> [!NOTE]  
>  REVOKE ALL 語法已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 改為撤銷特定的權限。  
  
 PRIVILEGES  
 為符合 ISO 而包含這個項目。 不會變更 ALL 的行為。  
  
 *permission*  
 這是權限的名稱。 本主題稍後[安全性實體特定語法](#securable)所列的幾個主題，會描述權限與安全性實體的有效對應。  
  
 *column*  
 指定正在撤銷權限的資料表中資料行的名稱。 它必須用括號括住。  
  
 *class*  
 指定正在撤銷權限之安全性實體的類別。 範圍限定詞 **::** 為必要項目。  
  
 *securable*  
 指定正在撤銷權限的安全性實體。  
  
 TO | FROM *principal*  
 這是主體的名稱。 可以撤銷安全性實體權限的主體，隨著安全性實體而不同。 如需有效組合的詳細資訊，請參閱本主題稍後[安全性實體特定語法](#securable)中所列的主題。  
  
 CASCADE  
 指出目前正在撤銷的權限，也會從它被這個主體所授與的其他主體一起撤銷。 當您使用 CASCADE 引數時，必須也包括 GRANT OPTION FOR 引數。  
  
> [!CAUTION]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *principal*  
 您可使用 AS principal 子句，來表示要撤銷由您以外的主體所授與的權限。 例如，假設使用者 Mary 是 principal_id 12；使用者 Raul 是 principal 15。 Mary 和 Raul 都授與 Steven 這個使用者相同的權限。 sys.database_permissions 資料表會指出權限兩次，但每個權限都各有不同的 grantor_prinicpal_id 值。 Mary 可以使用 `AS RAUL` 子句撤銷權限，以移除 Raul 的授權。
 
在此陳述式中使用 AS 不代表能模擬其他使用者。  
  
## <a name="remarks"></a>Remarks  
 REVOKE 陳述式的完整語法相當複雜。 上方的語法圖已簡化，以強調其結構。 本主題稍後[安全性實體特定語法](#securable)所列的幾個主題，會描述撤銷特定安全性實體權限的完整語法。  
  
 REVOKE 陳述式可用來移除授與的權限，而 DENY 陳述式可用來避免主體透過 GRANT 取得特定權限。  
  
 授與權限會移除指定安全性實體權限的 DENY 或 REVOKE。 如果相同權限在包含安全性實體的更高範圍被拒絕，則 DENY 的優先順序較高。 然而，在更高範圍撤銷授與權限的優先順序並不會比較高。  
  
> [!CAUTION]  
>  資料表層級的 DENY 不會優先於資料行層級的 GRANT。 保留權限階層中這項不一致的目的，是為了與舊版相容。 未來的版本將予以移除。  
  
 sp_helprotect 系統預存程序會報告資料庫層級安全性實體的權限。  
  
 從被授與指定了 GRANT OPTION 之權限的主體撤銷權限時，如果未指定 CASCADE，REVOKE 陳述式便會失敗。  
  
## <a name="permissions"></a>權限  
 具有安全性實體之 CONTROL 權限的主體可以撤銷安全性實體的權限。 物件擁有者可以撤銷他們所擁有之物件的權限。  
  
 CONTROL SERVER 權限的被授與者 (例如系統管理員 (sysadmin) 固定伺服器角色的成員)，可以撤銷伺服器中任何安全性實體的任何權限。 資料庫之 CONTROL 權限的被授與者 (例如 db_owner 固定資料庫角色的成員)，可以撤銷資料庫中任何安全性實體的任何權限。 結構描述之 CONTROL 權限的被授與者，可以撤銷結構描述中任何物件的任何權限。  
  
##  <a name="securable"></a> 安全性實體特定語法  
 下表列出安全性實體和描述安全性實體特定語法的主題。  
  
|安全性實體|主題|  
|---------------|-----------|  
|應用程式角色|[REVOKE 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|組件|[REVOKE 組件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-assembly-permissions-transact-sql.md)|  
|非對稱金鑰|[REVOKE 非對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-asymmetric-key-permissions-transact-sql.md)|  
|可用性群組|[REVOKE 可用性群組權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)|  
|憑證|[REVOKE 憑證權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-certificate-permissions-transact-sql.md)|  
|合約|[REVOKE Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|[資料庫]|[REVOKE 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-permissions-transact-sql.md)|  
|端點|[REVOKE 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)|  
|資料庫範圍認證|[REVOKE 資料庫範圍認證 (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)|  
|全文檢索目錄|[REVOKE 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|全文檢索停用字詞表|[REVOKE 全文檢索權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-full-text-permissions-transact-sql.md)|  
|函數|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|登入|[REVOKE 伺服器主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)|  
|訊息類型|[REVOKE Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|Object|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|佇列|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|遠端服務繫結|[REVOKE Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|角色|[REVOKE 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|路由|[REVOKE Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|結構描述|[REVOKE 結構描述權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-schema-permissions-transact-sql.md)|  
|搜尋屬性清單|[REVOKE 搜尋屬性清單權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-search-property-list-permissions-transact-sql.md)|  
|[伺服器]|[REVOKE 伺服器權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)|  
|服務|[REVOKE Service Broker 權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-service-broker-permissions-transact-sql.md)|  
|預存程序|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|對稱金鑰|[REVOKE 對稱金鑰權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)|  
|同義字|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|系統物件|[REVOKE 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)|  
|Table|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|類型|[REVOKE 類型權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)|  
|使用者|[REVOKE 資料庫主體權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)|  
|檢視|[REVOKE 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)|  
|XML 結構描述集合|[REVOKE XML 結構描述集合權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-xml-schema-collection-permissions-transact-sql.md)|  
  
## <a name="see-also"></a>另請參閱  
 [權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_adduser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)  
  
  
