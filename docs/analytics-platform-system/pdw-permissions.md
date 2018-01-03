---
title: "PDW 權限 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e271980-bec8-424b-9f68-cea11b4e64e8
caps.latest.revision: "23"
ms.openlocfilehash: 49bcb7cf5e8d4bb03acd9db5de87716ec2462191
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-permissions"></a>PDW 權限
本主題說明的需求和選項，來管理 SQL Server PDW 的資料庫權限。  
  
## <a name="BackupRestoreBasics"></a>資料庫引擎權限的基本概念  
伺服器層級透過登入，以及資料庫使用者與使用者定義資料庫角色的資料庫層級管理 SQL Server PDW 上的資料庫引擎權限。  
  
**登入**  
登入都是個別使用者帳戶，登入 SQL Server PDW。 SQL Server PDW 支援使用 Windows 驗證和 SQL Server 驗證登入。  Windows 驗證登入可以是 Windows 使用者或來自 SQL Server PDW 信任任何網域的 Windows 群組。 SQL Server 驗證登入所定義且由 SQL Server PDW 驗證，而且必須藉由指定密碼中建立。  
  
成員**sysadmin**固定的伺服器角色 (例如**sa**登入) 而不需要對應到資料庫使用者可以連接到資料庫。 對應至**dbo**使用者。 資料庫的擁有者也會對應為**dbo**使用者。  
  
**伺服器角色**  
有四個預先設定的角色，其提供方便的伺服器層級權限群組的一組特殊的伺服器角色。 **Sysadmin**， **MediumRC**， **LargeRC**，和**XLargeRCfixed**伺服器角色是目前實作 SQL 中唯一的伺服器角色Server PDW。 **Sa**登入是唯一的成員**sysadmin**固定的伺服器角色與其他登入不能加入至**sysadmin**角色。 授與登入**CONTROL SERVER**權限，這會很類似，但不完全相同**sysadmin**固定的伺服器角色。 使用[ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md)將成員新增至其他伺服器角色。 SQL Server PDW 不支援使用者定義伺服器角色。  
  
**資料庫使用者**  
登入授與資料庫的存取權的資料庫中建立資料庫使用者，並將該資料庫使用者對應至登入。 資料庫使用者名稱通常會與登入名稱相同，但這兩種名稱不一定非得相同。 每個資料庫使用者皆會對應至單一登入。 登入僅可對應至一個資料庫中的單一使用者，但其可對應做為數個不同資料庫中的資料庫使用者。  
  
**固定的資料庫角色**  
固定的資料庫角色是一組預先設定的角色，其提供方便的資料庫層級權限群組。 若要使用的固定的資料庫角色，則可以加入資料庫使用者與使用者定義資料庫角色[sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)程序。 如需有關固定的資料庫角色的詳細資訊，請參閱[固定資料庫角色](#fixed-database-roles)。  
  
**使用者定義資料庫角色**  
具有使用者**CREATE ROLE**權限可以建立新的使用者定義資料庫角色，以代表具有通用權限的使用者群組。 通常會針對整個角色授與或拒絕權限，以精簡權限管理與監視作業。  
  
權限授與至安全性主體 （登入、 使用者和角色） 使用**GRANT**陳述式。 使用明確拒絕權限**拒絕**命令。 使用移除先前授與或拒絕權限是**撤銷**陳述式。 權限會累計，使用者會接收授與至使用者登入以及任何群組成員資格的所有權限；不過，任何權限拒絕皆會覆寫所有授與。 <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
下列範例表示通用和建議的權限設定方法。  
  
1.  如果使用 Windows 驗證，請建立每個 Windows 使用者或 Windows 群組將會連接到 SQL Server PDW 的登入。 如果使用 SQL Server 驗證，請建立將會連接到 SQL Server PDW 的每個人的登入。  
  
2.  建立所有必要的資料庫中的每個登入的資料庫使用者。  
  
3.  建立一或多個使用者定義資料庫角色，分別代表類似的函式。 例如財務分析師和銷售分析師。  
  
4.  將資料庫使用者新增至一個或多個使用者定義資料庫角色。  
  
5.  授與權限至使用者定義資料庫角色。  
  
登入是伺服器層級物件，可以藉由檢視列出[sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。 只有伺服器層級權限可以授與伺服器主體。  
  
使用者與資料庫角色是資料庫層級物件，可以藉由檢視列出[sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)。 只有資料庫層級權限可授與資料庫主體。  
  
## <a name="BackupTypes"></a>預設權限  
下列清單描述預設權限：  
  
-   當登入由 using **CREATE LOGIN**陳述式中，登入會收到**CONNECT SQL**允許登入的權限連接到 SQL Server PDW。  
  
-   使用建立資料庫使用者時**CREATE USER**陳述式中，使用者會收到**CONNECT ON DATABASE::***< 資料庫名稱 >*權限，允許若要連接至該資料庫的使用者身分登入。  
  
-   所有的主體，包括公用角色中，依預設有沒有明確或隱含的權限，因為隱含權限繼承自明確權限。 因此，當沒有明確的權限時，可以也沒有隱含的權限。  
  
-   當登入成為的物件或資料庫擁有者時，登入一律具有物件或資料庫上的所有權限。 無法顯示為 明確權限的擁有權權限。 **GRANT**，**撤銷**，和**拒絕**陳述式沒有任何作用，擁有權權限。 可以透過變更擁有權[ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)陳述式。  
  
-   Sa 登入應用裝置上擁有的所有權限。 類似於擁有權，sa 權限無法變更，而且不會顯示做為明確的權限。 **GRANT**，**撤銷**，和**拒絕**陳述式都有 sa 權限不會影響。  
  
-   PUBLIC 伺服器角色預設會收到沒有權限，並沒有繼承自其他伺服器角色的權限。 PUBLIC 伺服器角色可以獲得明確權限及**GRANT**，**撤銷**，和**拒絕**陳述式。  
  
-   交易不需要權限。 可以執行所有主體**BEGIN TRANSACTION**，**認可**，和**復原**交易命令。 但是，主體必須具有適當的權限來執行交易內的每個陳述式。  
  
-   **使用**陳述式不需要權限。 可以執行所有主體**使用**陳述式上任何資料庫，不過若要存取資料庫它們必須擁有使用者主體在資料庫中，或必須啟用 guest 使用者。  
  
### <a name="the-public-role"></a>PUBLIC 角色  
所有新的應用裝置登入自動屬於 PUBLIC 角色。 PUBLIC 伺服器角色具有下列特性：  
  
-   PUBLIC 伺服器角色有預設沒有權限。  
  
-   所有的主體就是 PUBLIC 伺服器角色的成員以及 PUBLIC 伺服器角色不是另一個伺服器角色的成員。  
  
-   PUBLIC 伺服器角色無法繼承的隱含權限。 必須明確授與給 PUBLIC 角色提供的任何權限。  
  
## <a name="BackupProc"></a>判斷權限  
登入有權限執行特定動作而定的權限授與或拒絕登入、 使用者和角色的成員。 伺服器層級權限 (例如**CREATE LOGIN**和**VIEW SERVER STATE**) 可用於伺服器層級主體 （登入）。 資料庫層級權限 (例如**選取**從資料表或**EXECUTE**程序上) 可使用資料庫層級主體 （使用者和資料庫角色）。  
  
### <a name="implicit-and-explicit-permissions"></a>隱含和明確權限  
*明確權限*是**GRANT**或**拒絕**權限提供給主體的**授與**或**拒絕**陳述式。 資料庫層級權限詳列於[sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)檢視。 伺服器層級權限詳列於[sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)檢視。  
  
*隱含的權限*是**GRANT**或**拒絕**主體 （登入或伺服器角色） 已繼承的權限。 權限可以下列方式繼承。  
  
-   主體可以繼承的權限角色如果主體是角色的成員，即使沒有明確主體**GRANT**或**拒絕**權限。  
  
-   如果主體有其中一個物件的父系領域 （例如資料表或整個資料庫上的權限的結構描述） 上的權限的主體可以繼承 （例如資料表） 的從屬物件權限。  
  
-   主體可以擁有包含從屬權限的權限繼承的權限。 例如**ALTER ANY USER**權限同時包括**CREATE USER**和**ALTER ON USER::**  *<name>* 權限。  
  
### <a name="determining-permissions-when-performing-actions"></a>執行動作時，判斷權限  
決定哪些權限，指派給主體的程序相當複雜。 判斷隱含權限，因為主體可以是多個角色的成員和權限可傳遞多個層級角色階層中時，就會發生的複雜性。  
  
下列清單描述一般的規則，以判斷權限：  
  
-   擁有權隱含權限。  
  
    物件擁有者具有物件的所有權限。 同樣地，資料庫擁有者在資料庫中有所有資料庫的權限和物件的所有權限。 無法變更這些權限。  
  
-   可以跨多個層級，階層中的伺服器角色成員資格繼承權限。  
  
    例如，假設您有下列情況：  
  
    -   登入 David 是 PerfAnalysts 的資料庫角色的成員。  
  
    -   PerfAnalysts 是實際執行的資料庫角色的成員。  
  
    -   David 和 PerfAnalysts 沒有**選取**客戶資料表的權限。 權限已被撤銷，或者永遠不會明確授與。  
  
    -   有生產**選取**客戶資料表的權限。  
  
    在此情況下，將會繼承 PerfAnalysts**授與**與生產環境中，David 客戶資料表的權限將會繼承**授與**從生產環境的客戶資料表的權限。  
  
-   **拒絕**會覆寫**GRANT**當發生衝突的權限。  
  
    例如，假設 登入 David 客戶資料表上有任何權限，而且是兩個資料庫角色的成員 – dbgroup1，具有**拒絕**Customer 資料表和 dbgroup2，有權限**授與**客戶資料表上的權限。 在此情況下，將會繼承 David**拒絕**客戶資料表的權限。 這種是否角色在明確或隱含地取得其權限。  
  
### <a name="auditing-permissions"></a>稽核的權限  
若要研究的使用者權限檢查下列項目。  
  
-   執行下列查詢來判斷哪些登入是系統管理員。  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   執行下列查詢來判斷哪些登入已獲得明確權限。  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   若要判斷哪些資料庫使用者是資料庫角色的成員使用者資料庫中執行下列查詢。  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   執行下列查詢來判斷哪一個資料庫使用者與角色已被授與或拒絕特定權限的使用者資料庫中。 您必須查詢的其他檢視，例如 sys.objects 與 sys.schemas，藉此識別使用，則 major_id 就所述的項目。  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>資料庫權限的最佳作法  
  
-   授與權限在最細微的層級，以此。 授與的權限，在資料表或檢視層級權限可能會難以管理。 但在資料庫層級授與的權限可能會太寬鬆。 如果資料庫設計與結構描述來定義工作界限，可能是結構描述的授與權限會是適當洩露資料表層級和資料庫層級之間。  
  
-   授與權限給角色，而非使用者或登入。 管理使用而不是使用者角色的權限讓您更輕鬆快速地授與或撤銷移入或移出角色的使用者或登入的權限集。 當到另一個人傳遞函式時，權限可以保留在角色層級角色的成員資格變更時。  
  
-   授與權限給依據工作函式，以及較高層級的群組角色結合根據公司群組執行動作的工作函式角色的角色。  
  
-   每個使用者都應該有唯一的登入。 不允許使用者共用的登入。 提供每個使用者的登入可確保稽核記錄，並簡化權限管理。  
  
## <a name="fixed-database-roles"></a>固定資料庫角色
SQL Server 提供預先設定 （固定） 可協助您管理的伺服器上的權限的資料庫層級角色。 預先設定的角色被固定的因為您無法變更指派給他們的權限。 也可以建立使用者定義資料庫角色。 您可以變更指派給使用者定義資料庫角色的權限。  
  
角色是分組其他主體的安全性主體。 資料庫角色是全資料庫的權限範圍。 為資料庫角色的成員可以加入資料庫使用者與其他資料庫角色。 無法加入固定的資料庫角色彼此。 (「角色」就像是 Windows 作業系統中的「群組」)。  
  
有 9 固定的資料庫角色。  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>固定的資料庫角色的權限  
固定的伺服器角色與固定的資料庫角色的系統是來自於 1980's年舊有系統。 固定的角色仍然支援，並會有幾個使用者且簡單的安全性需求的環境中很有用。 從 SQL Server 2005 開始，授與權限的更詳細的系統已建立。 這個新的系統是更精細，授與和拒絕權限提供更多選擇。 更細微的系統的額外複雜性更難以了解，但大多數的企業系統應該授與權限，而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->下圖顯示與每個固定的資料庫角色相關聯的權限。 可用的 （或必要的） 不是這個 SQL Server 圖形中的所有權限 ap。  
  
![APS 安全性固定資料庫角色](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>相關內容  
  
-   若要建立使用者定義的角色，請參閱[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)。  
  
  
## <a name="fixed-server-roles"></a>固定伺服器角色
SQL Server 固定的伺服器角色會自動建立。 SQL Server PDW 具有有限的 SQL Server 固定伺服器角色實作。 只有**sysadmin**和**公用**擁有做為成員的使用者登入。 **Setupadmin**和**dbcreator**角色會在內部使用 SQL Server PDW。 無法加入其他成員，或從任何角色中移除。  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin 固定伺服器角色  
**sysadmin** 固定伺服器角色的成員可以執行伺服器中的所有活動。 **Sa**登入是唯一的成員**sysadmin**固定的伺服器角色。 無法加入其他登入**sysadmin**固定的伺服器角色。 授與**CONTROL SERVER**權限近似於中的成員資格**sysadmin**固定的伺服器角色。 下列範例會授與**CONTROL SERVER**權限的登入名為 Fay。  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> **CONTROL SERVER**權限提供的 SQL Server PDW 的幾乎完整控制權。 可能的話，請改為提供更細微的權限給登入。 例如，請考慮授與**VIEW SERVER STATE**， **ALTER ANY LOGIN**， **VIEW ANY DATABASE**，或**CREATE ANY DATABASE**權限。  
  
### <a name="public-server-role"></a>public 伺服器角色  
每一個登入可以連接到 SQL Server PDW 是屬於**公用**伺服器角色。 所有登入繼承授與的權限**公用**任何物件。 只能指派**公用**時想要提供給所有使用者物件的物件權限。 您無法變更成員資格**公用**角色。  
  
> [!NOTE]  
> **公用**實作方式與其他角色不同。 因為所有的伺服器主體的公開、 成員資格的成員**公用**中未列出角色**sys.server_role_members** DMV。  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>固定的伺服器角色與授與權限  
固定的伺服器角色與固定的資料庫角色的系統是來自於 1980's年舊有系統。 固定的角色仍然支援，並會有幾個使用者且簡單的安全性需求的環境中很有用。 從 SQL Server 2005 開始，授與權限的更詳細的系統已建立。 這個新的系統是更精細，授與和拒絕權限提供更多選擇。 更細微的系統的額外複雜性更難以了解，但大多數的企業系統應該授與權限，而不是使用固定的角色。 <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>相關主題  
  
- [授與權限](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

