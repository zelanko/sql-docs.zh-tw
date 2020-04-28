---
title: 權限
description: 本文說明針對平行處理資料倉儲管理資料庫許可權的需求和選項。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 499ac56d8a462f62dac92b97654a9ace12bd356e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289686"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>管理平行處理資料倉儲中的許可權
本文說明用來管理 SQL Server PDW 的資料庫許可權的需求和選項。

## <a name="database-engine-permission-basics"></a><a name="BackupRestoreBasics"></a>資料庫引擎許可權的基本概念
SQL Server PDW 的資料庫引擎許可權會透過登入在伺服器層級進行管理，並透過資料庫使用者和使用者定義的資料庫角色在資料庫層級進行管理。

**Logins**登入登入是用來登入 SQL Server PDW 的個別使用者帳戶。 SQL Server PDW 支援使用 Windows 驗證和 SQL Server Authentication 的登入。  Windows 驗證登入可以是 SQL Server PDW 所信任之任何網域中的 Windows 使用者或 Windows 群組。 SQL Server 驗證登入是由 SQL Server PDW 定義和驗證，而且必須藉由指定密碼來建立。

**系統管理員（sysadmin** ）固定伺服器角色的成員（例如**sa**登入）可以連接到資料庫，而不需要對應到資料庫使用者。 它們會對應至**dbo**使用者。 資料庫的擁有者也會對應為**dbo**使用者。

**伺服器角色**有四個特殊的伺服器角色具有一組預先設定的角色，可提供方便的伺服器層級許可權群組。 [ **Sysadmin**]、[ **MediumRC**]、[ **LargeRC**] 和 [ **XLargeRCfixed**伺服器] 角色是目前在 SQL Server PDW 中實作為唯一的伺服器角色。 **Sa**登入是**系統管理員（sysadmin** ）固定伺服器角色的唯一成員，而且無法將其他登入加入至**系統管理員（sysadmin** ）角色。 登入可以被授與**系統管理員（sysadmin** ）固定伺服器角色的**CONTROL SERVER**許可權，但這也是相同的，但並不完全相同。 使用 [ [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) ] 將成員加入至其他伺服器角色。 SQL Server PDW 不支援使用者定義的伺服器角色。

**資料庫使用者**藉由在資料庫中建立資料庫使用者，並將該資料庫使用者對應至登入，即可授與資料庫的存取權。 資料庫使用者名稱通常會與登入名稱相同，但這兩種名稱不一定非得相同。 每個資料庫使用者皆會對應至單一登入。 登入僅可對應至一個資料庫中的單一使用者，但其可對應做為數個不同資料庫中的資料庫使用者。

**固定資料庫角色**固定資料庫角色是一組預先設定的角色，可提供方便的資料庫層級許可權群組。 您可以使用[sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)程式，將資料庫使用者和使用者定義的資料庫角色加入至固定資料庫角色。 如需固定資料庫角色的詳細資訊，請參閱[固定資料庫角色](#fixed-database-roles)。

**使用者定義資料庫角色**具有「**建立角色**」許可權的使用者可以建立新的使用者定義資料庫角色，以代表具有通用許可權的使用者群組。 通常會針對整個角色授與或拒絕權限，以精簡權限管理與監視作業。

許可權會藉由使用**GRANT**語句，授與安全性主體（登入、使用者和角色）。 許可權會使用**DENY**命令明確拒絕。 先前授與或拒絕的許可權會藉由使用**REVOKE**語句來移除。 權限會累計，使用者會接收授與至使用者登入以及任何群組成員資格的所有權限；不過，任何權限拒絕皆會覆寫所有授與。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->

下列範例表示通用和建議的權限設定方法。

1.  如果使用 Windows 驗證，請為每個將連接到 SQL Server PDW 的 Windows 使用者或 Windows 群組建立登入。 如果使用 SQL Server 驗證，請為將連接至 SQL Server PDW 的每個人員建立登入。

2.  針對所有必要資料庫中的每個登入建立資料庫使用者。

3.  建立一或多個使用者定義資料庫角色，分別代表類似的函式。 例如財務分析師和銷售分析師。

4.  將資料庫使用者加入至一個或多個使用者定義的資料庫角色。

5.  授與權限至使用者定義資料庫角色。

登入是伺服器層級物件，而且可以藉由查看 sys.databases 來列出。 [server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 只有伺服器層級的許可權可以授與伺服器主體。

使用者和資料庫角色是資料庫層級物件，而且可以藉由查看[sys.databases](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)來列出。 database_principals。 只有資料庫層級許可權可以授與資料庫主體。

## <a name="default-permissions"></a><a name="BackupTypes"></a>預設權限
下列清單說明預設權限：

-   當使用**CREATE login**語句來建立登入時，登入會收到**connect SQL**許可權，讓登入能夠連接到 SQL Server PDW。

-   使用**CREATE user**語句建立資料庫使用者時，使用者會收到**database：：** _<database_name>_ 許可權的 connect，讓登入能夠以使用者的身分連接到該資料庫。

-   根據預設，所有主體（包括 PUBLIC 角色）都沒有明確或隱含許可權，因為隱含許可權是繼承自明確許可權。 因此，沒有明確的許可權時，也可能沒有隱含許可權。

-   當登入成為物件或資料庫的擁有者時，登入會一律擁有物件或資料庫的擁有權限。 擁有權許可權不會顯示為明確許可權。 **GRANT**、 **REVOKE**和**DENY**語句不會影響擁有權許可權。 您可以使用[ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)語句來變更擁有權。

-   sa 登入具有應用裝置的所有權限。 類似於擁有權權限，sa 權限無法變更，且會作為隱含權限而不會顯示。 **GRANT**、 **REVOKE**和**DENY**語句不會影響 sa 許可權。

-   PUBLIC 伺服器角色預設不會收到任何許可權，也不會繼承其他伺服器角色的許可權。 公用伺服器角色可以透過**GRANT**、 **REVOKE**和**DENY**語句提供明確許可權。

-   交易不需要許可權。 所有主體都可以執行**BEGIN TRANSACTION**、 **COMMIT**和**ROLLBACK** TRANSACTION 命令。 不過，主體必須具有適當的許可權，才能在交易內執行每個語句。

-   **USE** 陳述式不需要權限。 所有主體都可以在任何資料庫上執行**USE**語句，但是若要存取資料庫，他們必須擁有資料庫中的使用者主體，或是必須啟用 guest 使用者。

### <a name="the-public-role"></a>PUBLIC 角色
所有新的設備登入都會自動屬於 PUBLIC 角色。 公用伺服器角色具有下列特性：

-   PUBLIC 伺服器角色預設沒有許可權。

-   所有主體都是公用伺服器角色的成員，而公用伺服器角色則不是另一個伺服器角色的成員。

-   公用伺服器角色無法繼承隱含許可權。 必須明確授與提供給 PUBLIC 角色的任何許可權。

## <a name="determining-permissions"></a><a name="BackupProc"></a>判斷許可權
登入是否有執行特定動作的許可權，取決於授與或拒絕使用者為其成員之登入、使用者和角色的許可權。 伺服器層級的許可權（例如**CREATE LOGIN**和**VIEW SERVER STATE**）可用於伺服器層級主體（登入）。 資料庫層級的許可權（例如從資料表中**選取**或在程式上**執行**）可用於資料庫層級主體（使用者和資料庫角色）。

### <a name="implicit-and-explicit-permissions"></a>隱含和明確權限
「明確權限」** 是藉由 **GRANT** 或 **DENY** 陳述式來賦予主體的 **GRANT** 或 **DENY** 權限。 資料庫層級許可權會列在 [ [database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) ] 視圖中。 伺服器層級許可權會列在 [ [server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) ] 視圖中。

*隱含許可權*是主體（登入或伺服器角色）已繼承的**授**與或**拒絕**許可權。 許可權可以透過下列方式來繼承。

-   如果主體是角色的成員，即使主體沒有明確**授**與或**拒絕**許可權，主體也可以繼承角色的許可權。

-   主體可以繼承從屬物件（例如資料表）的許可權（如果主體具有其中一個物件父範圍的許可權（例如，資料表的架構或整個資料庫的許可權）。

-   主體可以藉由擁有包含次級許可權的許可權來繼承許可權。 例如， **ALTER ANY user**許可權同時包含**CREATE user**和**alter ON USER：：** _<name>_ 許可權。

### <a name="determining-permissions-when-performing-actions"></a>在執行動作時判斷許可權
判斷要指派給主體之許可權的程式很複雜。 判斷隱含許可權時，會發生複雜性，因為主體可以是多個角色的成員，而且可以透過角色階層中的多個層級傳遞許可權。

下列清單說明用來判斷許可權的一般規則：

-   擁有權意指許可權。

    物件擁有者具有物件的擁有權限。 同樣地，資料庫擁有者具有資料庫的擁有權限，以及資料庫中物件的擁有權限。 這些許可權無法變更。

-   在伺服器角色成員資格的階層中，可以跨多個層級繼承許可權。

    例如，假設您有下列情況：

    -   登入 David 是資料庫角色 PerfAnalysts 的成員。

    -   PerfAnalysts 是資料庫角色生產的成員。

    -   David 和 PerfAnalysts 沒有 Customer 資料表的**SELECT**許可權。 已撤銷或從未明確授與許可權。

    -   生產環境具有 Customer 資料表的**SELECT**許可權。

    在此情況下，PerfAnalysts 會從生產環境繼承 Customer 資料表的**grant**許可權，而 David 會從生產環境繼承 customer 資料表的**grant**許可權。

-   當權限衝突時，**拒絕**覆寫**GRANT** 。

    例如，假設登入 David 沒有 Customer 資料表的許可權，而且是兩個資料庫角色的成員-dbgroup1，其具有 Customer 資料表的**DENY**許可權，而 Dbgroup2 具有 customer 資料表的**GRANT**許可權。 在此情況下，David 會繼承 Customer 資料表的**DENY**許可權。 無論角色是以明確或隱含方式取得其許可權，都是如此。

### <a name="auditing-permissions"></a>審核許可權
若要研究使用者的許可權，請檢查下列各項。

-   執行下列查詢，以判斷哪些登入是系統管理員。

    ```sql
    SELECT SPLogins.name, 'is a member of ', SPRoles.name 
    FROM sys.server_role_members AS SRM 
    JOIN sys.server_principals AS SPRoles 
        ON SRM.role_principal_id = SPRoles.principal_id 
    JOIN sys.server_principals AS SPLogins 
        ON SRM.member_principal_id = SPLogins.principal_id;
    ```

-   執行下列查詢，以判斷已授與明確許可權的登入。

    ```sql
    SELECT name, 'has the ', state_desc , permission_name, ' permission'
    FROM sys.server_permissions AS SP
    JOIN sys.server_principals AS SPRoles 
        ON SP.grantee_principal_id = SPRoles.principal_id;
    ```

-   在使用者資料庫中執行下列查詢，以判斷哪些資料庫使用者是資料庫角色的成員。

    ```sql
    SELECT DPUsers.name, 'is a member of ', DPRoles.name  
    FROM sys.database_role_members AS DRM
    JOIN sys.database_principals AS DPRoles 
        ON DRM.role_principal_id = DPRoles.principal_id
    JOIN sys.database_principals AS DPUsers
        ON DRM.member_principal_id = DPUsers.principal_id;
    ```

-   在使用者資料庫中執行下列查詢，以判斷已授與或拒絕哪些資料庫使用者和角色的特定許可權。 您必須查詢其他視圖，例如 sys.databases 和 sys.databases，以識別 major_id 所描述的專案。

    ```sql
    SELECT DPUsers.name, 'has the ', permission_name, 
    'permission on the item described as class = ', class, 'id = ', major_id
    FROM sys.database_permissions AS DP
    JOIN sys.database_principals AS DPUsers
        ON DP.grantee_principal_id = DPUsers.principal_id;
    ```

## <a name="database-permissions-best-practices"></a><a name="RestoreProc"></a>資料庫許可權最佳做法

-   以最細微的層級授與許可權。 授與資料表或 view 層級許可權的許可權可能會變得難以管理。 但授與資料庫層級的許可權可能會過於寬鬆。 如果資料庫是以定義工作界限的架構來設計，也許授與架構的許可權是資料表層級和資料庫層級之間的適當折衷。

-   授與許可權給角色，而不是使用者或登入。 使用角色而不是使用者來管理許可權，可讓使用者或登入的許可權快速授與或撤銷，方法是將其移入或移出角色。 當函式從一個人傳遞至另一個人員時，許可權會在角色成員資格變更時保持不變。

-   根據執行動作的公司群組，將許可權授與以工作函式為基礎的角色，以及在較高層級的群組角色上，將工作函式角色結合在一起。

-   每個終端使用者都應該有唯一的登入。 不允許使用者共用登入。 為每個使用者提供登入，可確保審核記錄並簡化版權管理。

## <a name="fixed-database-roles"></a>固定資料庫角色
SQL Server 提供預先設定（固定）的資料庫層級角色，協助您管理伺服器上的許可權。 預先設定的角色是固定的，因為您無法變更指派給它們的許可權。 您也可以建立使用者定義的資料庫角色。 您可以變更指派給使用者定義資料庫角色的許可權。

角色是分組其他主體的安全性主體。 資料庫角色在其許可權範圍內是以資料庫為範圍。 資料庫使用者和其他資料庫角色可以加入為資料庫角色的成員。 固定資料庫角色無法加入彼此。 (「角色」** 就像是 Windows 作業系統中的「群組」**)。

有9個固定的資料庫角色。

-   **db_owner**

-   **db_securityadmin**

-   **db_accessadmin**

-   **db_backupoperator**

-   **db_ddladmin**

-   **db_datawriter**

-   **db_datareader**

-   **db_denydatawriter**

-   **db_denydatareader**

### <a name="permissions-of-the-fixed-database-roles"></a>固定資料庫角色的許可權
固定伺服器角色和固定資料庫角色的系統是在1980的中產生的舊版系統。 已修正的角色仍然受支援，而且在有少數使用者和安全性需求很簡單的環境中很有用。 從 SQL Server 2005 開始，會建立更詳細的授與許可權系統。 這個新系統更精細，同時提供更多的選項來授與和拒絕許可權。 較細微的系統的額外複雜性讓它更難以學習，但大部分的企業系統都應該授與許可權，而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->下圖顯示與每個固定資料庫角色相關聯的許可權。 此 SQL Server 圖形中的擁有權限都無法在 AP 中使用（或需要）。

![APS 安全性固定資料庫角色](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")

### <a name="related-content"></a>相關內容

-   若要建立使用者定義的角色，請參閱[建立角色](../t-sql/statements/create-role-transact-sql.md)。


## <a name="fixed-server-roles"></a>固定伺服器角色
固定伺服器角色會由 SQL Server 自動建立。 SQL Server PDW 具有有限的 SQL Server 固定伺服器角色的執行。 只有**系統管理員（sysadmin** ）和**公用**使用者會以成員身分登入。 SQL Server PDW，會在內部使用**setupadmin**和**dbcreator**角色。 無法在任何角色中新增或移除其他成員。

### <a name="sysadmin-fixed-server-role"></a>系統管理員（sysadmin）固定伺服器角色
**sysadmin** 固定伺服器角色的成員可以執行伺服器中的所有活動。 **Sa**登入是**系統管理員（sysadmin** ）固定伺服器角色的唯一成員。 無法將其他登入加入至**系統管理員（sysadmin** ）固定伺服器角色。 授與 **CONTROL SERVER** 權限會近似於 **sysadmin** 固定伺服器角色中的成員資格。 下列範例會將**CONTROL SERVER**許可權授與名為 Fay 的登入。

```sql
USE master;
GO
GRANT CONTROL SERVER TO Fay;
```

> [!IMPORTANT]
> **CONTROL SERVER**許可權幾乎可以完全控制 SQL Server PDW。 可能的話，請改為提供更細微的登入許可權。 例如，請考慮授與**VIEW 伺服器狀態**、**改變任何登**入、**查看任何資料庫**，或**建立任何資料庫**許可權。

### <a name="public-server-role"></a>公用伺服器角色
可以連接到 SQL Server PDW 的每一個登入都是**公用**伺服器角色的成員。 所有登入皆會繼承授與給任何物件之**public**的許可權。 只有當您希望物件可供所有使用者使用時，才指派物件的**公用**許可權。 您無法變更**public**角色中的成員資格。

> [!NOTE]
> **public**的執行方式與其他角色不同。 因為所有伺服器主體都是公用成員，所以不會在**server_role_members** DMV 中列出**public**角色的成員資格。

### <a name="fixed-server-roles-vs-granting-permissions"></a>固定伺服器角色與授與許可權
固定伺服器角色和固定資料庫角色的系統是在1980的中產生的舊版系統。 已修正的角色仍然受支援，而且在有少數使用者和安全性需求很簡單的環境中很有用。 從 SQL Server 2005 開始，會建立更詳細的授與許可權系統。 這個新系統更精細，同時提供更多的選項來授與和拒絕許可權。 較細微的系統的額外複雜性讓它更難以學習，但大部分的企業系統都應該授與許可權，而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->

## <a name="related-topics"></a>[相關主題]

- [授與許可權](grant-permissions.md)

<!-- MISSING LINKS
## See Also
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)
-->

