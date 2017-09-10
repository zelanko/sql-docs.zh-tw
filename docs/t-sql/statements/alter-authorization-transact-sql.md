---
title: "ALTER AUTHORIZATION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31738dcb4eaf4676b4c0a34b13ee400e89333428
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-authorization-transact-sql"></a>ALTER AUTHORIZATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
\<class_type > 是要變更擁有者的實體安全性實體類別。 OBJECT 是預設值。    
    
|||    
|-|-|    
|OBJECT|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，Azure SQL 資料倉儲， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|    
|ASSEMBLY|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|ASYMMETRIC KEY|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|AVAILABILITY GROUP |**適用對象**： 透過 SQL Server 2012 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|
|CERTIFICATE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|CONTRACT|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|DATABASE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 如需詳細資訊，請參閱[ALTER 授權的資料庫](#AlterDB)下一節。|    
|ENDPOINT|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|FULLTEXT CATALOG|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|FULLTEXT STOPLIST|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|MESSAGE TYPE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|REMOTE SERVICE BINDING|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|ROLE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|ROUTE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SCHEMA|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，Azure SQL 資料倉儲， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。|    
|SEARCH PROPERTY LIST|**適用對象**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|SERVER ROLE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SERVICE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|    
|SYMMETRIC KEY|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|TYPE|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
|XML SCHEMA COLLECTION|**適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|    
    
 *entity_name*    
 這是實體的名稱。    
    
 *principal_name* |結構描述擁有者    
 擁有實體的安全性主體名稱。 資料庫物件必須由資料庫主體、資料庫使用者或角色所擁有。 伺服器物件 (例如資料庫) 必須由伺服器主體 (登入) 所擁有。 指定**結構描述擁有者**為*principal_name*来表示應該擁有物件的結構描述的主體所擁有的物件。    
    
## <a name="remarks"></a>備註    
 ALTER AUTHORIZATION 可用來變更具有擁有者之任何實體的擁有權。 資料庫包含的實體擁有權可傳送給任何資料庫層級主體。 伺服器層級實體的擁有權只能傳送給伺服器層級主體。    
    
> [!IMPORTANT]    
>  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，使用者可以擁有其他資料庫使用者所擁有之結構描述內含的 OBJECT 或 TYPE。 這是和舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不同的一項行為變更。 如需詳細資訊，請參閱[OBJECTPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/objectproperty-transact-sql.md)和[TYPEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md).    
    
 下列「物件」類型之結構描述所包含實體的擁有權可以傳送：資料表、檢視、函數、程序、佇列和同義字。    
    
 下列實體的擁有權無法傳送：連結伺服器、統計資料、條件約束、規則、預設值、觸發程序、[!INCLUDE[ssSB](../../includes/sssb-md.md)] 佇列、認證、資料分割函數、資料分割結構描述、資料庫主要金鑰、服務主要金鑰和事件通知。    
    
 下列安全性實體類別之成員的擁有權無法傳送：伺服器、登入、使用者、應用程式角色和資料行。    
    
 當您傳送結構描述包含之實體的擁有權時，SCHEMA OWNER 選項才有效。 SCHEMA OWNER 會將實體的擁有權傳送給其所在之結構描述的擁有者。 只有 OBJECT、TYPE 或 XML SCHEMA COLLECTION 類別的實體才會包含結構描述。    
    
 如果目標實體不是資料庫，且實體要傳送給新的擁有者，則會卸除目標的所有權限。    
    
> [!CAUTION]    
>  在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，結構描述的行為已經與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的行為不同。 假設結構描述相當於資料庫使用者的程式碼可能不會傳回正確的結果。 曾經使用下列任何一個 DDL 陳述式的資料庫中不應該使用舊的目錄檢視 (包括 sysobjects)：CREATE SCHEMA、ALTER SCHEMA、DROP SCHEMA、CREATE USER、ALTER USER、DROP USER、CREATE ROLE、ALTER ROLE、DROP ROLE、CREATE APPROLE、ALTER APPROLE、DROP APPROLE、ALTER AUTHORIZATION。 在曾經使用這些陳述式的任何一個資料庫中，您必須使用新的目錄檢視。 新的目錄檢視會考量 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中所導入的主體和結構描述的分隔。 如需目錄檢視的詳細資訊，請參閱[目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。    
    
 同時應注意下列項目：    
    
> [!IMPORTANT]    
>  若要尋找的物件擁有者的唯一可靠方式就是查詢**sys.objects**目錄檢視。 尋找類型之擁有者的唯一可靠方式就是使用 TYPEPROPERTY 函數。    
    
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
**適用對象**: [!INCLUDE[ssSQL15](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
### <a name="for-sql-server"></a>針對 SQL Server:  
**新的擁有者的需求：**   
新主體資料庫擁有者必須是下列其中一項：  
-   SQL Server 驗證登入。  
-   Windows 驗證登入的 Windows 使用者 （不是群組）。  
-   透過 Windows 驗證的登入，代表 Windows 群組驗證的 Windows 使用者。  
  
**執行 ALTER AUTHORIZATION 陳述式的人員的需求：**  
如果您不屬於**sysadmin**固定伺服器角色，您必須擁有至少 TAKE OWNERSHIP 權限的資料庫，且必須具有 IMPERSONATE 權限登入的新擁有者。   

### <a name="for-azure-sql-database"></a>Azure SQL 資料庫：  
**新的擁有者的需求：**   
新主體資料庫擁有者必須是下列其中一項：  
-   SQL Server 驗證登入。  
-   同盟的使用者 （不是群組） 出現在 Azure AD。  
-   受管理的使用者 （不是群組） 或出現在 Azure AD 應用程式。    

> [!NOTE]  
> 如果新擁有者是 Azure Active Directory 使用者，它無法存在於的資料庫新擁有者將會變成新的 DBO 中的使用者身分。 這類的 Azure AD 使用者必須先移除，從資料庫才能執行 ALTER AUTHORIZATION 陳述式將資料庫擁有權變更為新的使用者。 如需設定 Azure Active Directory 使用者與 SQL 資料庫的詳細資訊，請參閱[連接到 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。   
  
**執行 ALTER AUTHORIZATION 陳述式的人員的需求：**  
您必須連接到目標資料庫，以變更該資料庫的擁有者。  

下列類型的帳戶可以變更資料庫擁有者。 
* 服務層級主體登入。 （SQL Azure 系統管理員佈建的邏輯伺服器建立時）。  
* Azure SQL Server 的 Azure Active Directory 系統管理員。   
* 資料庫的目前擁有者。   
 
  
下表摘要說明的需求：  
  
執行程式  |Target  |結果    
---------|---------|---------  
SQL Server 驗證登入     |SQL Server 驗證登入         |成功  
SQL Server 驗證登入     |Azure AD 使用者         |失敗           
Azure AD 使用者     |SQL Server 驗證登入         |成功           
Azure AD 使用者     |Azure AD 使用者         |成功           
  
若要確認資料庫的擁有者 Azure AD 會執行下列 TRANSACT-SQL 命令在使用者資料庫中 (在此範例中`testdb`)。  
    
```    
SELECT CAST(owner_sid as uniqueidentifier) AS Owner_SID   
FROM sys.databases   
WHERE name = 'testdb';  
```    
    
輸出將會對應至指派給 Azure AD ObjectID 的識別碼 （例如 6D8B81F6-7C79-444C-8858-4AF896C03C67)`richel@cqclinic.onmicrosoft.com`  
資料庫擁有者的 SQL Server 驗證登入使用者時，請在 master 資料庫，以確認資料庫擁有者執行下列陳述式：  
    
```    
SELECT d.name, d.owner_sid, sl.name   
FROM sys.databases AS d  
JOIN sys.sql_logins AS sl  
ON d.owner_sid = sl.sid;  
    
```    
  
### <a name="best-practice"></a>最佳做法  
  
而不是使用 Azure AD 使用者做為個別擁有者的資料庫，使用 Azure AD 群組的成員身分**db_owner**固定的資料庫角色。 下列步驟，示範如何設定已停用的登入的資料庫擁有者，並讓 Azure Active Directory 群組 (`mydbogroup`) 的成員**db_owner**角色。 
1.  SQL server 登入為 Azure AD 系統管理員，以及變更已停用的 SQL Server 驗證登入資料庫的擁有者。 例如，從使用者資料庫中執行：  
  ```    
  ALTER AUTHORIZATION ON database::testdb TO DisabledLogin;  
  ```    
2.  建立 Azure AD 群組應該擁有資料庫，並將它做為使用者加入至使用者資料庫。 例如：  
  ```    
  CREATE USER [mydbogroup] FROM EXTERNAL PROVIDER;  
  ```    
3.  在使用者資料庫中新增至代表 Azure AD 群組中，使用者**db_owner**固定的資料庫角色。 例如：  
  ```    
  ALTER ROLE db_owner ADD MEMBER mydbogroup;  
  ```    
  
現在`mydbogroup`成員可以集中管理資料庫做為成員的**db_owner**角色。  
- 當從 Azure AD 群組中移除此群組的成員時，它們會自動遺失此資料庫的 dbo 權限。  
- 同樣地加入新成員時`mydbogroup`Azure AD 群組，他們會自動取得此資料庫的 dbo 存取權。  
  
若要檢查特定的使用者是否具有有效的 dbo 權限，讓使用者執行下列陳述式：  
    
```    
SELECT IS_MEMBER ('db_owner');  
```    
  
傳回值 1 表示使用者角色的成員。  
   
    
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
    
 如果物件的結構描述不包含的陳述式，過程[!INCLUDE[ssDE](../../includes/ssde-md.md)]會尋找使用者預設結構描述中的物件。 例如：    
    
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
 下列範例的每個變更的擁有者`Sprockets`資料表中`Parts`資料庫到資料庫使用者`MichikoOsada`。    
```    
ALTER AUTHORIZATION ON Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON dbo.Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::Sprockets TO MichikoOsada;    
ALTER AUTHORIZATION ON OBJECT::dbo.Sprockets TO MichikoOsada;    
```    
    
### <a name="f-changing-the-owner-of-a-database"></a>F. 變更資料庫擁有者    
 **適用對象**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]， [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。    
    
 下列範例會變更擁有者`Parts`登入的資料庫`MichikoOsada`。    
    
```    
ALTER AUTHORIZATION ON DATABASE::Parts TO MichikoOsada;    
```    
  
### <a name="g-changing-the-owner-of-a-sql-database-to-an-azure-ad-user"></a>G. 將 SQL 資料庫的擁有者變更為 Azure AD 使用者  
在下列範例中，SQL Server 的 Azure Active Directory 系統管理員具有名為 active directory 的組織中`cqclinic.onmicrosoft.com`，可以變更目前的資料庫擁有權`targetDB`並讓 AAD 使用者`richel@cqclinic.onmicorsoft.com`新資料庫擁有者使用下列命令：  
    
```    
ALTER AUTHORIZATION ON database::targetDB TO [rachel@cqclinic.onmicrosoft.com];   
```    
    
 請注意，Azure AD 使用者必須使用方括號括住使用者名稱。  
  
    
## <a name="see-also"></a>另請參閱    
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)     
 [TYPEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)     
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)    
 

