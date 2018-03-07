---
title: "授與拒絕撤銷 Perms Azure SQL 資料與平行資料倉儲 |Microsoft 文件"
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
# <a name="permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse"></a>權限： GRANT、 DENY、 REVOKE （Azure SQL 資料倉儲，Parallel Data Warehouse）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **GRANT**和**拒絕**授與或拒絕權限的陳述式 (例如**更新**) 上的安全性實體 （例如資料庫、 資料表、 檢視等。)使用安全性主體 （登入、 資料庫使用者或資料庫角色）。 使用**撤銷**移除授與或拒絕的權限。  
  
 伺服器層級權限會套用至登入。 資料庫層級權限會套用至資料庫使用者與資料庫角色。  
  
 若要查看哪些權限已授與及拒絕，查詢 sys.server_permissions 與 sys.database_permissions 以及檢視。 未明確授與或拒絕安全性主體的權限可以在具有權限的角色具有成員資格繼承。 固定的資料庫角色的權限無法變更，而且不會出現在 sys.server_permissions 與 sys.database_permissions 檢視中。  
  
-   **授與**明確授與一或多個權限。  
  
-   **拒絕**明確地從一個或多個權限可拒絕主體。  
  
-   **撤銷**移除現有**GRANT**或**拒絕**權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 \<權限 > [ **，**...*n* ]  
 一或多個權限授與、 拒絕或撤銷。  
  
 ON [ \<class_type >::]*安全* **ON**子句描述安全性實體的參數，來授與、 拒絕或撤銷的權限。  
  
 \<class_type > 安全性實體的類別類型。 這可以是**登入**，**資料庫**，**物件**，**結構描述**，**角色**，或**使用者**. 權限也可授與 **SERVER * * * class_type*，但**伺服器**未指定這些權限。 **資料庫**未指定的權限時包含這個字**資料庫**(例如**ALTER ANY DATABASE**)。 若未*class_type*指定並不限於伺服器或資料庫類別的權限類型，此類別會被假設為**物件**。  
  
 *securable*  
 拒絕或撤銷的權限登入、 資料庫、 資料表、 檢視、 結構描述、 程序、 角色或要授與，使用者的名稱。 物件名稱可以使用三部分命名規則中所述來指定[TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
 若要*主體*[ **，**...*n* ]  
 一或多個主體授與、 拒絕或撤銷權限。 原則是登入、 資料庫使用者或資料庫角色的名稱。  
  
 從*主體*[ **，**...*n* ]  
 一或多個主體來撤銷權限。  原則是登入、 資料庫使用者或資料庫角色的名稱。 **從**僅能與**撤銷**陳述式。 **若要**可以搭配**GRANT**，**拒絕**，或**撤銷**。  
  
 WITH GRANT OPTION  
 指出也會提供被授與者授與指定權限給其他主體的能力。  
  
 CASCADE  
 指出權限遭到拒絕或撤銷對指定主體和所有其他主體的主體授與權限。 當主體具有的權限時，需要**GRANT OPTION**。  
  
 GRANT OPTION FOR  
 表示將撤銷授與指定權限的能力。 這是必要的當您使用**CASCADE**引數。  
  
> [!IMPORTANT]  
>  如果主體有不含指定的權限**GRANT**選項，則會撤銷權限本身。  
  
## <a name="permissions"></a>Permissions  
 授與權限，授與者必須具有權限本身與**WITH GRANT OPTION**，或必須具有隱含目前正在授與的權限的更高權限。  物件擁有者可以授與他們所擁有之物件的權限。 具有主體**控制項**安全性實體的權限可以授與權限在該安全性實體。  成員**db_owner**和**db_securityadmin**固定的資料庫角色可授與資料庫的任何權限。  
  
## <a name="general-remarks"></a>一般備註  
 拒絕或撤銷權限的主體不會影響已經過授權，而目前正在執行要求。 若要限制存取，您必須取消使用中要求或終止目前的工作階段。  
  
> [!NOTE]  
>  無法在此版本中使用最固定的伺服器角色。 請改用使用者定義資料庫角色。 無法加入登入**sysadmin**固定的伺服器角色。 授與**CONTROL SERVER**權限近似於中的成員資格**sysadmin**固定的伺服器角色。  
  
 某些陳述式需要多項權限。 例如，若要建立資料表需要**CREATE TABLE**權限在資料庫中，而**ALTER SCHEMA**資料表將包含資料表的權限。  
  
 PDW 有時會執行預存程序，將使用者動作來計算節點。 因此，您無法拒絕整個資料庫的 execute 權限。 (例如`DENY EXECUTE ON DATABASE::<name> TO <user>;`將會失敗。)因應措施，以拒絕 execute 權限的使用者結構描述或特定物件 （程序）。  
  
### <a name="implicit-and-explicit-permissions"></a>隱含和明確權限  
 *明確權限*是**GRANT**或**拒絕**權限提供給主體的**授與**或**拒絕**陳述式。  
  
 *隱含的權限*是**GRANT**或**拒絕**主體 （登入、 使用者或資料庫角色） 具有繼承自另一個資料庫角色的權限。  
  
 隱含的權限也可以繼承自涵蓋或父系使用權限。 例如，**更新**資料表的權限可讓繼承**更新**包含資料表的結構描述權限或**控制項**資料表的權限。  
  
### <a name="ownership-chaining"></a>擁有權鏈結  
 當多個資料庫物件以循序方式存取時，稱為序列*鏈結*。 雖然此類鏈結不會獨立存在，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 周遊鏈結中的連結時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 評估要素物件權限的方式，與單獨存取物件時不同。 擁有權鏈結有重要的影響，用於管理安全性。 如需有關擁有權鏈結的詳細資訊，請參閱[擁有權鏈結](http://msdn.microsoft.com/en-us/library/ms188676\(v=sql11\).aspx)和[教學課程： 擁有權鏈結和內容切換](http://msdn.microsoft.com/en-us/library/bb153640\(v=sql11\).aspx)。  
  
## <a name="permission-list"></a>權限清單  
  
### <a name="server-level-permissions"></a>伺服器層級權限  
 伺服器層級權限可以授與、 拒絕及撤銷登入。  
  
 **將套用至伺服器的權限**  
  
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
  
 **套用至登入權限**  
  
-   登入控制  
  
-   登入的 ALTER  
  
-   模擬登入  
  
-   VIEW DEFINITION  
  
### <a name="database-level-permissions"></a>資料庫層級權限  
 資料庫層級權限可以授與，已拒絕及撤銷資料庫使用者與使用者定義資料庫角色。  
  
 **適用於所有的資料庫類別的權限**  
  
-   CONTROL  
  
-   ALTER  
  
-   VIEW DEFINITION  
  
 **套用至所有資料庫的類別，但是使用者權限**  
  
-   TAKE OWNERSHIP  
  
 **僅適用於資料庫的權限**  
  
-   ALTER ANY DATABASE  
  
-   針對 DATABASE 的 ALTER  
  
-   ALTER ANY DATASPACE  
  
-   ALTER ANY ROLE  
  
-   ALTER ANY SCHEMA  
  
-   ALTER ANY USER  
  
-   BACKUP DATABASE  
  
-   在資料庫連接  
  
-   CREATE PROCEDURE  
  
-   CREATE ROLE  
  
-   CREATE SCHEMA  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
-   SHOWPLAN  
  
 **僅適用於使用者的權限**  
  
-   IMPERSONATE  
  
 **適用於資料庫、 結構描述和物件的權限**  
  
-   ALTER  
  
-   DELETE  
  
-   執行 CREATE 陳述式之前，請先執行  
  
-   INSERT  
  
-   SELECT  
  
-   UPDATE  
  
-   參考  
  
 如需每種類型的權限的定義，請參閱[權限 (Database Engine)](http://msdn.microsoft.com/library/ms191291.aspx)。  
  
### <a name="chart-of-permissions"></a>權限的圖表  
 所有的權限以圖形方式呈現這張海報上。 這是最簡單的方式來查看巢狀的階層的權限。 例如**ALTER ON LOGIN**可以授與權限本身，但它也包含如果授與登入**控制項**權限登入，或如果授與登入**ALTER ANY登入**權限。  
  
 ![APS 安全性權限海報](../../t-sql/statements/media/aps-security-perms-poster.png "APS 安全性權限海報")  
  
 若要下載此海報的完整大小版本，請參閱[SQL Server PDW 權限](http://go.microsoft.com/fwlink/?LinkId=244249)AP Yammer 網站的 [檔案] 區段中 (或要求所來自的電子郵件 **apsdoc@microsoft.com** 。  
  
## <a name="default-permissions"></a>預設權限  
 下列清單描述預設權限：  
  
-   當登入由使用**CREATE LOGIN**陳述式會收到新的登入**CONNECT SQL**權限。  
  
-   所有登入都屬於**公用**伺服器角色，且無法移除從**公用**。  
  
-   使用建立資料庫使用者時**CREATE USER**權限，資料庫使用者會收到**連接**資料庫的權限。  
  
-   所有的主體，包括**公用**角色，預設有沒有明確或隱含的權限。  
  
-   當登入或使用者成為資料庫或物件的擁有者時，登入或使用者永遠具有資料庫或物件的所有權限。 無法變更擁有權權限，而且不會顯示做為明確的權限。 **GRANT**，**拒絕**，和**撤銷**陳述式都有擁有者不會影響。  
  
-   **Sa**登入應用裝置上擁有的所有權限。 類似於擁有權的權限， **sa**權限無法變更，而且不會顯示做為明確的權限。 **GRANT**，**拒絕**，和**撤銷**陳述式沒有任何作用**sa**登入。 **Sa**無法重新命名登入。  
  
-   **使用**陳述式不需要權限。 可以執行所有主體**使用**上任何資料庫的陳述式。  
  
##  <a name="Examples"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-granting-a-server-level-permission-to-a-login"></a>A. 授與伺服器層級權限的登入  
 下列兩個陳述式授與至登入伺服器層級權限。  
  
```  
GRANT CONTROL SERVER TO [Ted];  
```  
  
```  
GRANT ALTER ANY DATABASE TO Mary;  
```  
  
### <a name="b-granting-a-server-level-permission-to-a-login"></a>B. 授與伺服器層級權限的登入  
 下列範例會授與伺服器層級權限的登入伺服器主體 （另一個登入）。  
  
```  
GRANT  VIEW DEFINITION ON LOGIN::Ted TO Mary;  
```  
  
### <a name="c-granting-a-database-level-permission-to-a-user"></a>C. 資料庫層級權限授與使用者  
 下列範例會授與資料庫層級權限以資料庫主體 （另一位使用者）。  
  
```  
GRANT VIEW DEFINITION ON USER::[Ted] TO Mary;  
```  
  
### <a name="d-granting-denying-and-revoking-a-schema-permission"></a>D. 授與、 拒絕與撤銷結構描述權限  
 下列**GRANT**陳述式授與 Yuen 從任何資料表或檢視 dbo 結構描述中的選取資料的能力。  
  
```  
GRANT SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 下列**拒絕**陳述式可防止 Yuen 從任何資料表或檢視 dbo 結構描述中的選取資料。 Yuen 無法讀取資料，即使他有權限，以其他方式，例如透過角色成員資格。  
  
```  
DENY SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
 下列**撤銷**陳述式移除**拒絕**權限。 現在則中性 Yuen 的明確權限。 Yuen 可以透過等角色的成員資格的其他某些隱含權限的任何資料表選取資料。  
  
```  
REVOKE SELECT ON SCHEMA::dbo TO [Yuen];  
```  
  
### <a name="e-demonstrating-the-optional-object-clause"></a>E. 示範的選擇性物件:: 子句  
 因為物件的權限陳述式的預設類別，下列兩個陳述式都相同。 **物件::**子句是選擇性的。  
  
```  
GRANT UPDATE ON OBJECT::dbo.StatusTable TO [Ted];  
```  
  
```  
GRANT UPDATE ON dbo.StatusTable TO [Ted];  
```  
  
  

