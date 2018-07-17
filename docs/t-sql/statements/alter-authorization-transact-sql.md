---
title: ALTER AUTHORIZATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_AUTHORIZATION_TSQL
- ALTER AUTHORIZATION
dev_langs:
- TSQL
helpviewer_keywords:
- owners [SQL Server], transferring
- modifying entity ownership
- full-text search [SQL Server], permissions
- owners [SQL Server], entities
- ALTER AUTHORIZATION statement
- entity ownership [SQL Server]
- transferring ownership
- search property lists [SQL Server], permissions
- TAKE OWNERSHIP
ms.assetid: 8c805ae2-91ed-4133-96f6-9835c908f373
caps.latest.revision: 84
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d1ff4bfeb848cf4f668d7e48a3cd3b574052ecc
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786209"
---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  變更安全性實體的擁有權。    
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>語法    
    
```    
-- Syntax for SQL Server  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
        OBJECT | ASSEMBLY | ASYMMETRIC KEY | AVAILABILITY GROUP | CERTIFICATE     
      | CONTRACT | TYPE | DATABASE | ENDPOINT | FULLTEXT CATALOG     
      | FULLTEXT STOPLIST | MESSAGE TYPE | REMOTE SERVICE BINDING    
      | ROLE | ROUTE | SCHEMA | SEARCH PROPERTY LIST | SERVER ROLE     
      | SERVICE | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

```
-- Syntax for SQL Database  
  
ALTER AUTHORIZATION    
   ON [ <class_type>:: ] entity_name    
   TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::=    
    {    
      OBJECT | ASSEMBLY | ASYMMETRIC KEY | CERTIFICATE     
    | TYPE | DATABASE | FULLTEXT CATALOG     
    | FULLTEXT STOPLIST     
    | ROLE | SCHEMA | SEARCH PROPERTY LIST     
    | SYMMETRIC KEY | XML SCHEMA COLLECTION    
    }    
```    

    
```    
-- Syntax for Azure SQL Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
```    
-- Syntax for Parallel Data Warehouse  
  
ALTER AUTHORIZATION ON    
    [ <class_type> :: ] <entity_name>     
    TO { principal_name | SCHEMA OWNER }    
[;]    
    
<class_type> ::= {    
      DATABASE     
    | SCHEMA     
    | OBJECT     
}    
    
<entity_name> ::=    
{    
      database_name 
    | schema_name    
    | [ schema_name. ] object_name    
}    
```    
    
## <a name="arguments"></a>引數    
\<class_type> 為變更擁有者之實體的安全性實體類別。 OBJECT 是預設值。    
    
|||    
|-|-|    
|OBJECT|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、Azure SQL 資料倉儲、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|    
|ASSEMBLY|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|ASYMMETRIC KEY|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|AVAILABILITY GROUP |**適用對象**：SQL Server 2012 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|
|CERTIFICATE|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|CONTRACT|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|DATABASE|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 如需詳細資訊，請參閱下方的[資料庫的 ALTER AUTHORIZATION](#AlterDB) 一節。|    
|ENDPOINT|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|FULLTEXT CATALOG|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|FULLTEXT STOPLIST|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|MESSAGE TYPE|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|REMOTE SERVICE BINDING|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|ROLE|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|ROUTE|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SCHEMA|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、Azure SQL 資料倉儲、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|    
|SEARCH PROPERTY LIST|**適用對象**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|SERVER ROLE|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SERVICE|**適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SYMMETRIC KEY|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|TYPE|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|XML SCHEMA COLLECTION|**適用對象**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
    
 *entity_name*    
 這是實體的名稱。    
    
 *principal_name* | SCHEMA OWNER    
 擁有實體的安全性主體名稱。 資料庫物件必須由資料庫主體、資料庫使用者或角色所擁有。 伺服器物件 (例如資料庫) 必須由伺服器主體 (登入) 所擁有。 指定 **SCHEMA OWNER** 作為 *principal_name*，表示物件必須由擁有物件結構描述的主體所擁有。    
    
## <a name="remarks"></a>Remarks    
 ALTER AUTHORIZATION 可用來變更具有擁有者之任何實體的擁有權。 資料庫包含的實體擁有權可傳送給任何資料庫層級主體。 伺服器層級實體的擁有權只能傳送給伺服器層級主體。    
    
> [!IMPORTANT]    
>  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，使用者可以擁有其他資料庫使用者所擁有之結構描述內含的 OBJECT 或 TYPE。 這是和舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不同的一項行為變更。 如需詳細資訊，請參閱 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md) 及 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)。    
    
 下列「物件」類型之結構描述所包含實體的擁有權可以傳送：資料表、檢視、函數、程序、佇列和同義字。    
    
 下列實體的擁有權無法傳送：連結伺服器、統計資料、條件約束、規則、預設值、觸發程序、[!INCLUDE[ssSB](../../includes/sssb-md.md)] 佇列、認證、資料分割函數、資料分割結構描述、資料庫主要金鑰、服務主要金鑰和事件通知。    
    
 下列安全性實體類別之成員的擁有權無法傳送：伺服器、登入、使用者、應用程式角色和資料行。    
    
 當您傳送結構描述包含之實體的擁有權時，SCHEMA OWNER 選項才有效。 SCHEMA OWNER 會將實體的擁有權傳送給其所在之結構描述的擁有者。 只有 OBJECT、TYPE 或 XML SCHEMA COLLECTION 類別的實體才會包含結構描述。    
    
 如果目標實體不是資料庫，且實體要傳送給新的擁有者，則會卸除目標的所有權限。    
    
> [!CAUTION]    
>  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，結構描述的行為已經與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的行為不同。 假設結構描述相當於資料庫使用者的程式碼可能不會傳回正確的結果。 曾經使用下列任何一個 DDL 陳述式的資料庫中不應該使用舊的目錄檢視 (包括 sysobjects)：CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 在曾經使用這些陳述式的任何一個資料庫中，您必須使用新的目錄檢視。 新的目錄檢視會考量 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中所導入的主體和結構描述的分隔。 如需目錄檢視的詳細資訊，請參閱[目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。    
    
 同時應注意下列項目：    
    
> [!IMPORTANT]    
>  尋找物件之擁有者的唯一可靠方式就是查詢 **sys.objects** 目錄檢視。 尋找類型之擁有者的唯一可靠方式就是使用 TYPEPROPERTY 函數。    
    
## <a name="special-cases-and-conditions"></a>特殊案例和條件    
 下表列出特殊案例、例外狀況和條件，這些都適用於改變授權。    
    
|類別|條件|    
|-----------|---------------|    
|OBJECT|無法變更觸發程序、條件約束、規則、預設值、統計資料、系統物件、佇列、索引檢視或具有索引檢視之資料表的擁有權。|    
|SCHEMA|當傳送擁有權時，將卸除沒有明確擁有者之結構描述所包含物件的權限。 無法變更 sys、dbo 或 information_schema 的擁有者。|    
|TYPE|無法變更屬於 sys 或 information_schema 之 TYPE 的擁有權。|    
|CONTRACT、MESSAGE TYPE 或 SERVICE|無法變更系統實體的擁有權。|    
|SYMMETRIC KEY|無法變更全域暫時金鑰的擁有權。|    
|CERTIFICATE 或 ASYMMETRIC KEY|無法將這些實體的擁有權傳送給角色或群組。|    
|ENDPOINT|主體必須是登入。|    
  
## <a name="AlterDB"></a>資料庫的 ALTER AUTHORIZATION  
**適用對象**：[!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
### <a name="for-sql-server"></a>針對 SQL Server：  
**新擁有者的需求：**   
新的擁有者主體必須是下列其中一項：  
-   SQL Server 驗證登入。  
-   表示 Windows 使用者的 Windows 驗證登入 (而非群組)。  
-   透過表示 Windows 群組之 Windows 驗證登入驗證的 Windows 使用者。  
  
**執行 ALTER AUTHORIZATION 陳述式的人員需求：**  
若您不是 **sysadmin** 固定伺服器角色的成員，您必須至少擁有資料庫的 TAKE OWNERSHIP 權限，並且必須擁有新擁有者登入的 IMPERSONATE 權限。   

### <a name="for-azure-sql-database"></a>針對 Azure SQL Database：  
**新擁有者的需求：**   
新的擁有者主體必須是下列其中一項：  
-   SQL Server 驗證登入。  
-   Azure AD 中存在的同盟使用者 (而非群組)。  
-   Azure AD 中存在的受控使用者 (而非群組) 或應用程式。    

> [!NOTE]  
> 若新的擁有者為 Azure Active Directory 使用者，它將無法在新的擁有者會成為新 DBO 的資料庫中作為使用者存在。 必須先從資料庫移除這類 Azure AD 使用者，才能執行 ALTER AUTHORIZATION 陳述式，將資料庫的擁有權變更為新的使用者。 如需使用 SQL Database 設定 Azure Active Directory 使用者的詳細資訊，請參閱[使用 Azure Active Directory 驗證連線到 SQL Database 或 SQL 資料倉儲](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。   
  
**執行 ALTER AUTHORIZATION 陳述式的人員需求：**  
您必須連線到目標資料庫，才能變更該資料庫的擁有者。  

下列帳戶類型可變更資料庫的擁有者。 
* 服務層級主體登入。 (建立邏輯伺服器時佈建的 SQL Azure 系統管理員。)  
* Azure SQL Server 的 Azure Active Directory 系統管理員。   
* 資料庫目前的擁有者。   
 
  
下表摘要這些需求：  
  
執行程式  |目標  |結果    
---------|---------|---------  
SQL Server 驗證登入     |SQL Server 驗證登入         |成功  
SQL Server 驗證登入     |Azure AD 使用者         |失敗           
Azure AD 使用者     |SQL Server 驗證登入         |成功           
Azure AD 使用者     |Azure AD 使用者         |成功           
  
若要驗證資料庫的 Azure AD 擁有者，請在使用者資料庫中執行下列 Transact-SQL 命令 (在此範例中為 `testdb`)。  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
輸出將為識別碼 (例如 6D8B81F6-7C79-444C-8858-4AF896C03C67)，該識別碼會對應到指派給 `richel@cqclinic.onmicrosoft.com` 的 Azure AD ObjectID  
當 SQL Server 驗證登入使用者為資料庫擁有者時，請在 master 資料庫中執行下列陳述式來驗證資料庫擁有者：  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>最佳做法  
  
請使用 Azure AD 群組作為 **db_owner** 固定資料庫角色的成員，而非使用 Azure AD 使用者作為資料庫的個別擁有者。 下列步驟示範如何將已停用的登入設定為資料庫擁有者，並讓 Azure Active Directory 群組 (`mydbogroup`) 成為 **db_owner** 角色的成員。 
1.  以 Azure AD 系統管理員的身分登入 SQL Server，然後將資料庫的擁有者變更為已停用的 SQL Server 驗證登入。 例如，從使用者資料庫中執行：  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  建立應擁有資料庫的 Azure AD 群組，然後將其作為使用者新增至使用者資料庫。 例如：  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  在使用者資料庫中，將表示 Azure AD 群組的使用者新增至 **db_owner** 固定資料庫角色。 例如：  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
現在 `mydbogroup` 成員可作為 **db_owner** 角色的成員集中管理資料庫。  
- 當此群組的成員從 Azure AD 群組移除時，它們會自動喪失此資料庫的 dbo 權限。  
- 同樣的，若將新的成員新增至 `mydbogroup` Azure AD 群組，它們也會自動取得此資料庫的 dbo 存取。  
  
若要檢查特定使用者是否具備有效的 dbo 權限，請讓使用者執行下列陳述式：  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
傳回值若為 1 則表示使用者為角色的成員。  
   
    
## <a name="permissions"></a>Permissions    
 需要實體的 TAKE OWNERSHIP 權限。 如果新擁有者不是執行這個陳述式的使用者，而且需要 1) 新擁有者的 IMPERSONATE 權限 (如果它是使用者或登入的話)；或 2) 如果新擁有者是角色，則需要角色中的成員資格，或角色的 ALTER 權限；或 3) 如果新擁有者是應用程式角色，則需要應用程式角色的 ALTER 權限。    
    
## <a name="examples"></a>範例    
    
### <a name="a-transfer-ownership-of-a-table"></a>A. 轉移資料表的擁有權    
 下列範例會將資料表 `Sprockets` 的擁有權轉移給使用者 `MichikoOsada`。 此資料表位於結構描述 `Parts` 內。    
    
```    
ALTER AUTHORIZATION ON OBJECT::Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 這項查詢也會如下所示：    
    
```    
ALTER AUTHORIZATION ON Parts.Sprockets TO MichikoOsada;    
GO    
```    
    
 若物件結構描述並未作為陳述式的一部分包含在其中，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會在使用者預設結構描述中尋找物件。 例如：    
    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
```    
    
### <a name="b-transfer-ownership-of-a-view-to-the-schema-owner"></a>B. 將檢視的擁有權轉移給結構描述擁有者    
 下列範例會將 `ProductionView06` 檢視的擁有權轉移給包含其結構描述的擁有者。 此檢視位於結構描述 `Production` 內。    
    
```    
ALTER AUTHORIZATION ON OBJECT::Production.ProductionView06 TO SCHEMA OWNER;    
GO    
```    
    
### <a name="c-transfer-ownership-of-a-schema-to-a-user"></a>C. 將結構描述的擁有權轉移給使用者    
 下列範例會將 `SeattleProduction11` 結構描述的擁有權轉移給使用者 `SandraAlayo`。    
    
```    
ALTER AUTHORIZATION ON SCHEMA::SeattleProduction11 TO SandraAlayo;    
GO    
```    
    
### <a name="d-transfer-ownership-of-an-endpoint-to-a-sql-server-login"></a>D. 將端點的擁有權轉移給 SQL Server 登入    
 下列範例會將 `CantabSalesServer1` 端點的擁有權轉移給 `JaePak`。 因為端點是伺服器層級安全性實體，所以端點只能傳送給伺服器層級主體。    
    
**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。    
    
```    
ALTER AUTHORIZATION ON ENDPOINT::CantabSalesServer1 TO JaePak;    
GO    
```    
    
### <a name="e-changing-the-owner-of-a-table"></a>E. 變更資料表的擁有者    
 下列每個範例都會將 `Parts` 資料庫中 `Sprockets` 資料表的擁有者變更為 `MichikoOsada` 資料庫使用者。    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. 變更資料庫的擁有者    
 **適用對象**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。    
    
 下列範例會將 `Parts` 資料庫的擁有者變更為 `MichikoOsada` 登入。    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. 將 SQL Database 的擁有者變更為 Azure AD 使用者  
在下列範例中，具有名為 `cqclinic.onmicrosoft.com` 之 Active Directory 組織中的 SQL Server Azure Active Directory 系統管理員，可變更 `targetDB` 資料庫目前的擁有權，並使用下列命令讓 `richel@cqclinic.onmicorsoft.com` AAD 使用者成為新的資料庫擁有者：  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 請注意，針對 Azure AD 使用者，使用者名稱必須以括弧括住。  
  
    
## <a name="see-also"></a>另請參閱    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 
