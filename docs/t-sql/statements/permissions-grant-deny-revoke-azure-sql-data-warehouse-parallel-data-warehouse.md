---
title: "GRANT-DENY-REVOKE 權限 - Azure SQL 資料倉儲和平行處理資料倉儲 | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5a3b7424-408e-4cb0-8957-667ebf4596fc
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c46d4df3d19b2c548b203f62a14ea4ebc0226296
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>權限：GRANT、DENY、REVOKE (Azure SQL 資料倉儲、平行處理資料倉儲)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]的 **GRANT** 和 **DENY** 陳述式，以針對安全性主體 (登入、資料庫使用者或資料庫角色) 授與或拒絕對安全性實體 (例如資料庫、資料表、檢視等) 的權限 (例如 **UPDATE**)。 使用 **REVOKE** 來移除某個權限的授與或拒絕。  
  
 伺服器層級權限會套用至登入。 資料庫層級權限會套用至資料庫使用者和資料庫角色。  
  
 若要查看已授與或拒絕哪些權限，請查詢 sys.server_permissions 和 sys.database_permissions 檢視。 未以明確方式對安全性主體授與或拒絕的權限，可藉由擁有具權限之角色的成員資格來繼承。 固定資料庫角色的權限無法變更，且不會顯示在 sys.server_permissions 和 sys.database_permissions 檢視中。  
  
-   **GRANT** 會明確授與一或多個權限。  
  
-   **DENY** 會對主體明確拒絕一或多個權限。  
  
-   **REVOKE** 會移除現有的 **GRANT** 或 **DENY** 權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
GRANT   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
[;]  
  
DENY   
    <permission> [ ,...n ]  
    [ ON [ <class_type> :: ] securable ]   
    TO principal [ ,...n ]  
    [ CASCADE ]  
[;]  
  
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
 \<permission>[ **,**...*n* ]  
 一或多個要授與、拒絕或撤銷的權限。  
  
 ON [ \<class_type> :: ] *securable* **ON** 子句描述要作為授與、拒絕或撤銷權限時之執行對象的 securable 參數。  
  
 \<class_type> 安全性實體的類別類型。 這可以是 **LOGIN**、**DATABASE**、**OBJECT**、**SCHEMA**、**ROLE** 或 **USER**。 您也可以將權限授與 **SERVER***class_type*，但針對這些權限不需指定 **SERVER**。 當權限包含 **DATABASE** 一字 (例如 **ALTER ANY DATABASE**) 時，不需指定 **DATABASE**。 未指定任何 *class_type* 且權限類型未限制為伺服器或資料庫類別時，會假設類別為 **OBJECT**。  
  
 *securable*  
 要作為授與、拒絕或撤銷權限時之執行對象的登入、資料庫、資料表、檢視、結構描述、程序、角色或使用者的名稱。 指定物件名稱時，可以使用 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)中所述的三部分命名規則來指定。  
  
 TO *principal* [ **,**...*n* ]  
 一或多個被授與、拒絕或撤銷權限的主體。 主體是登入、資料庫使用者或資料庫角色的名稱。  
  
 FROM *principal* [ **,**...*n* ]  
 一或多個要撤銷權限的主體。  主體是登入、資料庫使用者或資料庫角色的名稱。 **FROM** 只能與 **REVOKE** 陳述式搭配使用。 **TO** 可以與 **GRANT****DENY**或 **REVOKE**搭配使用。  
  
 WITH GRANT OPTION  
 指出也會提供被授與者授與指定權限給其他主體的能力。  
  
 CASCADE  
 表示對指定的主體及被主體授與權限的所有其他主體拒絕或撤銷權限。 當主體擁有含 **GRANT OPTION** 的權限時，這是必要引數。  
  
 GRANT OPTION FOR  
 表示將撤銷授與指定權限的能力。 當您使用 **CASCADE** 引數時，這是必要引數。  
  
> [!IMPORTANT]  
>  如果主體擁有不含 **GRANT** 選項的指定權限，則會撤銷權限本身。  
  
## <a name="permissions"></a>Permissions  
 若要授與權限，授與者必須具有含 **WITH GRANT OPTION** 的權限本身，或具有隱含所要授與之權限的更高權限。  物件擁有者可以授與他們所擁有之物件的權限。 具有安全性實體之 **CONTROL** 權限的主體可以授與該安全性實體的權限。  **db_owner** 和 **db_securityadmin** 固定資料庫角色的成員可以授與資料庫中的任何權限。  
  
## <a name="general-remarks"></a>一般備註  
 對主體拒絕或撤銷權限並不會影響已通過授權且目前正在執行的要求。 若要立即限制存取，您必須取消作用中的要求，或終止目前的工作階段。  
  
> [!NOTE]  
>  大多數固定伺服器角色在此版本中都無法使用。 請改用使用者定義的資料庫角色。 您無法將登入新增至 **sysadmin** 固定伺服器角色。 授與 **CONTROL SERVER** 權限會近似於 **sysadmin** 固定伺服器角色中的成員資格。  
  
 有些陳述式需要多個權限。 例如，若要建立資料表，需要資料庫中的 **CREATE TABLE** 權限，以及該資料表之上層資料表的 **ALTER SCHEMA** 權限。  
  
 PDW 有時會執行預存程序，以將使用者動作散發至計算集點。 因此，不能拒絕整個資料庫的執行權限。 (例如 `DENY EXECUTE ON DATABASE::<name> TO <user>;` 會失敗)。因應之道就是拒絕對使用者結構描述或特定物件 (程序) 的執行權限。  
  
### <a name="implicit-and-explicit-permissions"></a>隱含和明確權限  
 「明確權限」 是藉由 **GRANT** 或 **DENY** 陳述式來賦予主體的 **GRANT** 或 **DENY** 權限。  
  
 「隱含權限」 是主體 (登入、使用者或資料庫角色) 從另一個資料庫角色繼承的 **GRANT** 或 **DENY** 權限。  
  
 隱含權限也可以繼承自涵蓋權限或父權限。 例如，藉由擁有資料表之上層結構描述的 **UPDATE** 權限或資料表的 **CONTROL** 權限，即可繼承資料表的 **UPDATE** 權限。  
  
### <a name="ownership-chaining"></a>擁有權鏈結  
 當多個資料庫物件依序存取彼此時，此順序即稱為「鏈結」。 雖然此類鏈結不會獨立存在，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 周遊鏈結中的連結時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 評估要素物件權限的方式，與單獨存取物件時不同。 擁有權鏈結對於管理安全性有很重要的影響。 如需有關擁有權鏈結的詳細資訊，請參閱[擁有權鏈結](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx)和[教學課程：擁有權鏈結和內容切換](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx)。  
  
## <a name="permission-list"></a>權限清單  
  
### <a name="server-level-permissions"></a>伺服器層級權限  
 您可以從登入授與、拒絕及撤銷伺服器層級權限。  
  
 **適用於伺服器的權限**  
  
-   CONTROL SERVER  
  
-   ADMINISTER BULK OPERATIONS  
  
-   ALTER ANY CONNECTION  
  
-   ALTER ANY DATABASE  
  
-   CREATE ANY DATABASE  
  
-   ALTER ANY EXTERNAL DATA SOURCE  
  
-   ALTER ANY EXTERNAL FILE FORMAT  
  
-   ALTER ANY LOGIN  
  
-   ALTER SERVER STATE  
  
-   CONNECT SQL  
  
-   VIEW ANY DEFINITION  
  
-   VIEW ANY DATABASE  
  
-   VIEW SERVER STATE  
  
 **適用於登入的權限**  
  
-   CONTROL ON LOGIN  
  
-   ALTER ON LOGIN  
  
-   IMPERSONATE ON LOGIN  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>資料庫層級權限  
 您可以從資料庫使用者和使用者定義的資料庫角色，授與、拒絕及撤銷資料庫層級權限。  
  
 **適用於所有資料庫類別的權限**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **適用於除了使用者以外所有資料庫類別的權限**  
  
-   TAKE OWNERSHIP  
  
 **僅適用於資料庫的權限**  
  
-   ALTER ANY DATABASE  
  
-   ALTER ON DATABASE  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   CONNECT ON DATABASE  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **僅適用於使用者的權限**  
  
-   IMPERSONATE  
  
 **適用於資料庫、結構描述及物件的權限**  
  
-   ALTER  
  
-   DELETE  
  
-   EXECUTE  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   REFRENCES  
  
 如需了解每一種權限的定義，請參閱[權限 (資料庫引擎)](http://msdn.microsoft.com/library/ms191291.aspx)。  
  
### <a name="chart-of-permissions"></a>權限圖表  
 這張海報以圖形方式顯示所有權限。 這是了解權限巢狀階層的最簡單方式。 例如，**ALTER ON LOGIN** 權限可藉由本身授與，但如果登入被授與該登入的 **CONTROL** 權限，或如果登入被授與 **ALTER ANY LOGIN** 權限，則也會包含此權限。  
  
 ![APS 安全性權限海報](../../t-sql/statements/media/aps-security-perms-poster.png "APS 安全性權限海報")  
  
 若要下載這張海報的完整大小版本，請參閱 APS Yammer 網站之檔案區段中的 [SQL Server PDW 權限](http://go.microsoft.com/fwlink/?LinkId=244249) (或透過電子郵件向 **apsdoc@microsoft.com** 索取)。  
  
## <a name="default-permissions"></a>預設權限  
 下列清單說明預設權限：  
  
-   藉由使用 **CREATE LOGIN** 陳述式來建立登入時，新登入會收到 **CONNECT SQL** 權限。  
  
-   所有登入都是 **public** 伺服器角色的成員，且無法從 **public**中移除。  
  
-   藉由使用 **CREATE USER** 權限來建立資料庫使用者時，該資料庫使用者會收到資料庫中的 **CONNECT** 權限。  
  
-   所有主體 (包括 **public** 角色) 預設都沒有任何明確或隱含的權限。  
  
-   當登入或使用者成為資料庫或物件的擁有者時，登入或使用者一律會擁有該資料庫或物件的所有權限。 擁有權權限無法變更，且會作為隱含權限而不會顯示。 **GRANT**、**DENY** 及 **REVOKE** 陳述式對擁有者沒有任何作用。  
  
-   **sa** 登入具有應用裝置的所有權限。 類似於擁有權權限，**sa** 權限無法變更，且會作為隱含權限而不會顯示。 **GRANT**、**DENY** 及 **REVOKE** 陳述式對 **sa** 登入沒有任何作用。 您無法將 **sa** 登入重新命名。  
  
-   **USE** 陳述式不需要權限。 所有主體都可以在任何資料庫上執行 **USE** 陳述式。  
  
##  <a name="Examples"></a> 範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. 將伺服器層級權限授與登入  
 下列兩個陳述式會將伺服器層級權限授與某個登入。  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. 將伺服器層級權限授與登入  
 下列範例會將某個登入的伺服器層級權限授與某個伺服器主體 (另一個登入)。  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. 將資料庫層級權限授與使用者  
 下列範例會將某個使用者的資料庫層級權限授與某個資料庫主體 (另一個使用者)。  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. 授與、拒絕及撤銷結構描述權限  
 下列 **GRANT** 陳述式會讓 Yuen 能夠從 dbo 結構描述中的任何資料表或檢視中選取資料。  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 下列 **DENY** 陳述式會讓 Yuen 無法從 dbo 結構描述中的任何資料表或檢視中選取資料。 Yuen 即使藉由某個其他方式取得權限 (例如透過角色成員資格)，也無法讀取資料。  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 下列 **REVOKE** 陳述式會移除 **DENY** 權限。 現在 Yuen 的明確權限已變成中性。 Yuen 或許能夠透過某個其他隱含權限 (例如角色成員資格) 從任何資料表中選取資料。  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. 示範選擇性 OBJECT:: 子句  
 由於 OBJECT 是權限陳述式的預設類別，因此下列兩個陳述式相同。 **OBJECT::** 子句是選擇性的。  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

