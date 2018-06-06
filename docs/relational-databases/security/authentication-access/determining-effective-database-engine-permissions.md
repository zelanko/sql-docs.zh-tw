---
title: 判斷有效的 Database Engine 權限 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- permissions, effective
- effective permissions
ms.assetid: 273ea09d-60ee-47f5-8828-8bdc7a3c3529
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0a2e2c205558f81b2141739bdc9b53bbb85d55f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="determining-effective-database-engine-permissions"></a>判斷有效的 Database Engine 權限
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本文描述如何判斷哪些使用者具有 SQL Server 資料庫引擎中各種物件的權限。 SQL Server 會實作 Database Engine 的兩個權限系統。 舊的固定角色系統具有預先設定的權限。 從 SQL Server 2005 開始，提供更具彈性且更精確的系統 (本文的資訊適用於 SQL Server 2005 以上的版本。 有些版本的 SQL Server 無法使用某些類型的權限)。

>  [!IMPORTANT] 
>  * 有效的權限是兩個權限系統的彙總。 
>  * 拒絕權限會覆寫授與權限。 
>  * 如果使用者是 sysadmin 固定伺服器角色成員，則不會進一步檢查權限，因此不會強制執行拒絕。 
>  * 舊系統與新系統類似。 例如，`sysadmin` 固定伺服器角色中的成員資格會與具有 `CONTROL SERVER` 權限類似。 但是，系統不會完全相同。 例如，如果登入只有 `CONTROL SERVER` 權限，而且預存程序會檢查 `sysadmin` 固定伺服器角色中的成員資格，則權限檢查會失敗。 反之亦然。 


## <a name="summary"></a>摘要   
* 伺服器層級權限可以來自固定伺服器角色或使用者定義伺服器角色的成員資格。 每個人都屬於 `public` 固定伺服器角色，並接收該處指派的任何權限。   
* 伺服器層級權限可以來自權限授與或登入或是使用者定義伺服器角色。   
* 資料庫層級權限可以來自每個資料庫中固定資料庫角色或使用者定義資料庫角色的成員資格。 每個人都屬於 `public` 固定資料庫角色，並接收該處指派的任何權限。   
* 資料庫層級權限可以來自每個資料庫中的權限授與或登入或是使用者定義資料庫角色。   
* 權限可以接收自 `guest` 登入或 `guest` 資料庫使用者 (如果啟用的話)。 預設會停用 `guest` 登入和使用者。   
* Windows 使用者可以是具有登入資格的 Windows 群組成員。 Windows 使用者使用 Windows 群組安全性識別碼連線並顯示 Windows Token 時，SQL Server 會了解 Windows 群組成員資格。 因為 SQL Server 不會管理或接收 Windows 群組成員資格的自動更新，所以 SQL Server 無法可靠地報告接收自 Windows 群組成員資格的 Windows 使用者權限。   
* 切換至應用程式角色，並提供密碼，即可取得權限。   
* 執行包含 `EXECUTE AS` 子句的預存程序，即可取得權限。   
* 具有 `IMPERSONATE` 權限的登入或使用者可以取得權限。   
* 本機電腦系統管理員群組的成員一律可以將其權限提升至 `sysadmin` (不適用於 SQL Database)。  
* `securityadmin` 固定伺服器角色的成員可以提升其許多權限，而在某些情況下可以將權限提升至 `sysadmin` (不適用於 SQL Database)。   
* SQL Server 系統管理員可以查看所有登入和使用者的相關資訊。 權限較少的使用者通常只能看到自己的識別資訊。

## <a name="older-fixed-role-permission-system"></a>舊的固定角色權限系統

固定伺服器角色和固定資料庫角色具有預先設定且無法變更的權限。 若要判斷哪些使用者是固定伺服器角色成員，請執行下列查詢：    
>  [!NOTE] 
>  不適用於沒有伺服器層級權限的 SQL Database 或 SQL 資料倉儲。 SQL Server 2012 已新增 `sys.server_principals` 的 `is_fixed_role` 資料行。 舊版 SQL Server 則不需要。  
```sql
SELECT SP1.name AS ServerRoleName, 
 isnull (SP2.name, 'No members') AS LoginName   
 FROM sys.server_role_members AS SRM
 RIGHT OUTER JOIN sys.server_principals AS SP1
   ON SRM.role_principal_id = SP1.principal_id
 LEFT OUTER JOIN sys.server_principals AS SP2
   ON SRM.member_principal_id = SP2.principal_id
 WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
 ORDER BY SP1.name;
```
>  [!NOTE] 
>  * 所有登入都是 Public 角色的成員，且無法移除。 
>  * 這個查詢會檢查 master 資料庫中的資料表，但可以在內部部署產品的任何資料庫中執行。 

若要判斷誰是固定資料庫角色成員，請在每個資料庫中執行下列查詢。
```sql
SELECT DP1.name AS DatabaseRoleName, 
   isnull (DP2.name, 'No members') AS DatabaseUserName 
 FROM sys.database_role_members AS DRM
 RIGHT OUTER JOIN sys.database_principals AS DP1
   ON DRM.role_principal_id = DP1.principal_id
 LEFT OUTER JOIN sys.database_principals AS DP2
   ON DRM.member_principal_id = DP2.principal_id
 WHERE DP1.is_fixed_role = 1
 ORDER BY DP1.name;
```
若要了解授與每個角色的權限，請參閱《線上叢書》中圖例的角色描述 ([伺服器層級角色](../../../relational-databases/security/authentication-access/server-level-roles.md)和[資料庫層級角色](../../../relational-databases/security/authentication-access/database-level-roles.md))。

## <a name="newer-granular-permission-system"></a>新的細微權限系統

這個系統具有彈性，但如果設定人員講求精確的話，系統可能會比較複雜。 若要簡化事項，它有助於建立角色，並將權限指派給角色，然後將一群人新增至角色。 如果資料庫開發小組透過結構描述來區隔活動，接著將角色權限授與整個結構描述，而不是個別資料表或程序，則會比較容易。 真實世界的案例十分複雜，且商務需求可能會衍生非預期的安全性需求。   

[!INCLUDE[database-engine-permissions](../../../includes/paragraph-content/database-engine-permissions.md)]


### <a name="security-classes"></a>安全性類別

在伺服器層級、資料庫層級、結構描述層級或物件層級等等，可以授與權限。有 26 個層級 (稱為類別)。 依字母順序排列的完整類別清單如下：`APPLICATION ROLE`、`ASSEMBLY`、`ASYMMETRIC KEY`、`AVAILABILITY GROUP`、`CERTIFICATE`、`CONTRACT`、`DATABASE`、`DATABASE` `SCOPED CREDENTIAL`、`ENDPOINT`、`FULLTEXT CATALOG`、`FULLTEXT STOPLIST`、`LOGIN`、`MESSAGE TYPE`、`OBJECT`、`REMOTE SERVICE BINDING`、`ROLE`、`ROUTE`、`SCHEMA`、`SEARCH PROPERTY LIST`、`SERVER`、`SERVER ROLE`、`SERVICE`、`SYMMETRIC KEY`、`TYPE`、`USER`、`XML SCHEMA COLLECTION` (在某些類型的 SQL Server 上無法使用一些類別)。若要提供每個類別的完整資訊，則需要不同的查詢。

### <a name="principals"></a>主體

權限會授與主體。 主體可以是伺服器角色、登入、資料庫角色或使用者。 登入可以代表包含許多 Windows 使用者的 Windows 群組。 因為 Windows 群組不是由 SQL Server 維護，所以 SQL Server 不一定知道誰是 Windows 群組的成員。 Windows 使用者連線到 SQL Server 時，登入封包會包含使用者的 Windows 群組成員資格 Token。

Windows 使用者使用根據 Windows 群組的登入進行連線時，某些活動可能需要 SQL Server 建立登入或使用者來代表個別 Windows 使用者。 例如，Windows 群組 (Engineers) 包含使用者 (Mary、Todd、Pat)，而 Engineers 群組具有資料庫使用者帳戶。 如果 Mary 具有權限，並建立資料表，就可能將使用者 (Mary) 建立為資料表的擁有者。 或者，如果 Todd 被拒絕具有 Engineers 群組其他人所具有的權限，則必須建立使用者 Todd 以追蹤拒絕權限。

請記住，Windows 使用者可能是多個 Windows 群組 (例如 Engineers 和 Managers) 的成員。 授與或拒絕 Engineers 登入的權限、授與或拒絕 Managers 登入的權限、個別授與或拒絕使用者的權限，以及授與或拒絕使用者所屬角色的權限，全部都會予以彙總並評估是否為有效的權限。 `HAS_PERMS_BY_NAME` 函式可以顯示使用者還是登入具有特定權限。 不過，沒有明顯的方法可以判斷授與或拒絕權限的來源。 請研究權限清單，也可以使用試誤法進行實驗。

## <a name="useful-queries"></a>有用的查詢

### <a name="server-permissions"></a>伺服器權限

下列查詢會傳回一份已在伺服器層級授與或拒絕的權限清單。 這個查詢應該在 master 資料庫中執行。   
>  [!NOTE] 
>  在 SQL Database 或 SQL Data Warehouse 上，無法授與或查詢伺服器層級權限。   
```sql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
 FROM sys.server_principals AS pr
 LEFT OUTER JOIN sys.server_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
 ORDER BY pr.name, type_desc;
```

### <a name="database-permissions"></a>資料庫權限

下列查詢會傳回一份已在資料庫層級授與或拒絕的權限清單。 這個查詢應該在每個資料庫中執行。   
```sql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
FROM sys.database_principals AS pr
LEFT OUTER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0 
ORDER BY pr.name, type_desc;
```

可將權限資料表加入其他系統檢視的每個權限類別，而這些系統檢視提供該安全性實體類別的相關資訊。 例如，下列查詢會提供受到權限影響之資料庫物件的名稱。    
```sql
SELECT pr.type_desc, pr.name, pe.state_desc, 
 pe.permission_name, s.name + '.' + oj.name AS Object, major_id
 FROM sys.database_principals AS pr
 JOIN sys.database_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 JOIN sys.objects AS oj
   ON oj.object_id = pe.major_id
 JOIN sys.schemas AS s
   ON oj.schema_id = s.schema_id
 WHERE class_desc = 'OBJECT_OR_COLUMN';
```
使用 `HAS_PERMS_BY_NAME` 函式來判斷特定使用者 (在此情況下是 `TestUser`) 是否具有權限。 例如：   
```sql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```
如需語法的詳細資訊，請參閱 [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md)。

## <a name="see-also"></a>另請參閱：

[Database Engine 權限使用者入門](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)    
[教學課程：Database Engine 使用者入門](Tutorial:%20Getting%20Started%20with%20the%20Database%20Engine.md) 

