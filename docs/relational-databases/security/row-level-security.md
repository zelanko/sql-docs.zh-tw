---
title: 資料列層級安全性 | Microsoft 文件
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b150fa58725e157834c202224c679ee5119cdb8a
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="row-level-security"></a>資料列層級安全性
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  ![資料列層級安全性圖形](../../relational-databases/security/media/row-level-security-graphic.png "資料列層級安全性圖形")  
  
 資料列層級安全性可讓客戶能夠控制存取的使用者執行查詢 (例如，群組成員資格或執行內容) 的特性為基礎的資料庫資料表中的資料列。  
  
 資料列層級安全性 (RLS) 簡化您的應用程式中安全性的設計和編碼。 RLS 可讓您在資料列存取進行實作限制。 例如，確保工作者只能存取其部門的相關資料列，或限制僅能存取其公司的相關客戶資料。  
  
 存取限制邏輯是位於資料庫層，而不是離開這些資料，到另一個應用程式層。 資料庫系統會在每次於任何層嘗試存取該資料時套用存取限制。 透過減少安全性系統的介面區，讓您的安全性系統更可靠且健全。  
  
 使用 [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式以及作為[內嵌資料表值函數](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)的述詞來實作 RLS。  
  
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([立即取得](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag))。  
  

##  <a name="Description"></a> 描述  
 RLS 可支援兩種類型的安全性述詞。  
  
-   篩選器述詞以無訊息方式篩選可讀取作業 (SELECT、UPDATE 及 DELETE) 的資料列。  
  
-   Block 述詞會明確封鎖違反述詞的寫入作業 (AFTER INSERT、AFTER UPDATE、BEFORE UPDATE、BEFORE DELETE)。  
  
 定義為內嵌資料表值函數的安全性述詞，會限制資料表中資料列層級資料的存取權。 然後叫用函式並強制執行安全性原則。 對篩選述詞而言，沒有應用程式指示已從結果集篩選資料列；若所有資料列皆經過篩選，將會傳回 null 設定。 對 Block 述詞而言，任何違反述詞的作業都將會失敗並產生錯誤。  
  
 從基底資料表中讀取資料時會套用篩選器述詞，並且會影響所有取得作業：**SELECT**、**DELETE** (也就是使用者無法刪除篩選的資料列)，和 **UPDATE** (也就是使用者無法更新篩選的資料列，雖然您可以這樣更新資料列使其後續進行篩選)。 Block 述詞會影響所有寫入作業。  
  
-   AFTER INSERT 和 AFTER UPDATE 述詞可以防止使用者將資料列更新為違反述詞的值。  
  
-   BEFORE UPDATE 述詞可以防止使用者將資料列更新為目前違反述詞的值。  
  
-   BEFORE DELETE 述詞可以封鎖刪除作業。  
  
 篩選器述詞、Block 述詞及安全性原則皆具有下列行為：  
  
-   您可定義與另一個資料表聯結和/或叫用函數的述詞函數。 如果以 `SCHEMABINDING = ON`來建立安全性原則，則聯結或函數可從查詢存取，並且如預期般運作，而不需任何額外的權限檢查。 如果以 `SCHEMABINDING = OFF`來建立安全性原則，則使用者需要對這些額外的資料表和函數具有 **SELECT** 或 **EXECUTE** 權限，才能查詢目標資料表。
  
-   可對己定義但停用安全性述詞的資料表發出查詢。 不會影響任何屆時已篩選或封鎖的資料列。  
  
-   若 dbo 使用者、 **db_owner** 角色的成員，或資料表擁有者對已定義且啟用安全性原則的資料表進行查詢，資料列便會依安全性原則所定義而受到篩選或封鎖。  
  
-   若您嘗試變更結構描述繫結安全性原則所繫結資料表的結構描述，將會導致錯誤。 不過，您可以改變述詞不參考的資料行。  
  
-   若嘗試在已替指定作業定義述詞的資料表上加入述詞，不論該述詞的狀態為啟用或停用，都將產生錯誤。  
  
-   對結構描述繫結安全性原則而言，嘗試修改安全性原則中資料表上作為述詞的函數會導致錯誤。  
  
-   定義包含非重疊的述詞的多個作用中的安全性原則，就會成功。  
  
 篩選器述詞具有下列行為：  
  
-   定義篩選資料表的資料列的安全性原則。 應用程式不會察覺到任何已篩選出的資料列 **SELECT**， **UPDATE**，和 **DELETE** 作業，包括所有資料列已經篩選掉的情況。應用程式可以 **INSERT** 任何資料列，不論在任何其他作業期間是否進行篩選。  
  
 Block 述詞具有下列行為：  
  
-   UPDATE 的 Block 述詞會針對 BEFORE 和 AFTER 分割成個別的作業。 因此，比方說，您無法避免使用者將資料列更新為具有高於目前的值。 若需要此種邏輯，您必須搭配 DELETED 及 INSERTED 中繼資料表使用觸發程序，以同時參考舊值與新值。  
  
-   若述詞函數所使用的所有資料行皆未變更，最佳化工具便不會檢查 AFTER UPDATE Block 述詞。 例如︰Alice 應該無法將薪資變更為大於 100,000，但她應能變更薪資已超過 100,000 (因此已違反述詞) 之員工的地址。  
  
-   連同 BULK INSERT 在內的大量 API 皆未變更。 這表示 Block 述詞 AFTER INSERT 會套用至大量插入作業，就如同一般的插入作業。  
  
  
##  <a name="UseCases"></a> 使用案例  
 以下是如何使用 RLS 的設計範例：  
  
-   醫院可以建立安全性原則，讓護士僅能檢視各自病患的資料列。  
  
-   銀行可以根據員工的業務部門、或根據公司內部的員工職務建立一個原則，來限制財務資料列的存取權。  
  
-   多租用戶應用程式可以建立一個原則來強制執行邏輯分離每個租用戶的資料列與每個其他租用戶的資料列。 透過單一資料表中的多個租用戶資料的儲存體，可達到效率。 當然，每個租用戶只能看到它的資料列。  
  
 RLS 篩選述詞的功能等同於附加 **WHERE** 子句。 述詞可以像商務作法命令一樣為複雜，或子句可以像 `WHERE TenantId = 42`一樣簡單。  
  
 在更正式的用語，RLS 將介紹述詞型的存取控制。 其特色為彈性、 集中式、 述詞性的評估，依據適當情況，考量中繼資料或其他系統管理員決定的準則。 述詞作為準則，以根據使用者屬性判斷使用者是否具有適當的資料存取權。 標籤為基礎的存取控制可以使用述詞為基礎的存取控制來實作。  
  
  
##  <a name="Permissions"></a> 權限  
 建立、 改變或卸除安全性原則需要 **ALTER ANY SECURITY POLICY** 權限。 建立或卸除安全性原則需要 **ALTER** 結構描述權限。  
  
 此外，每個加入的述詞還需要下列權限：  
  
-   正做為述詞使用之函數**SELECT** 和 **REFERENCES** 權限。  
  
-   正繫結至原則之目標資料表的**REFERENCES** 權限。  
  
-   目標資料表中做為引數使用之每個資料行的**REFERENCES** 權限。  
  
 安全性原則套用到所有使用者，包括資料庫中的 dbo 使用者。 Dbo 使用者可以改變或卸除安全性原則，不過可稽核的安全性原則變更。 若高特殊權限的使用者 (例如系統管理員或 db_owner) 需要查看所有資料列，以進行疑難排解或驗證資料，則安全性原則必須寫入為允許這麼做。  
  
 如果以 `SCHEMABINDING = OFF`來建立安全性原則，則為了查詢目標資料表，使用者必須對述詞函數和述詞函數內使用的任何其他資料表、檢視或函數具有  **SELECT** 或 **EXECUTE** 權限。 如果以 `SCHEMABINDING = ON` (預設值) 來建立安全性原則，則當使用者查詢目標資料表時，會略過這些權限檢查。  
  
  
##  <a name="Best"></a> 最佳作法  
  
-   強烈建議建立 RLS 物件 (述詞函式和安全性原則) 的另一個結構描述。  
  
-   **ALTER ANY SECURITY POLICY** 權限是提供給高權限使用者 (例如安全性原則管理員) 。 安全性原則管理員不需要 **SELECT** 權限所保護的資料表。  
  
-   請避免在述詞函式中進行型別轉換，以避免可能的執行階段錯誤。  
  
-   盡量避免在述詞函數中使用遞迴，以免效能下降。 查詢最佳化工具會嘗試偵測直接遞迴，但是不一定能夠找出間接遞迴 (亦即，其中第二個函式呼叫述詞函式時)。  
  
-   請避免在述詞函式中使用過多的資料表聯結，將效能最大化。  
  
 避免述詞邏輯取決於工作階段特定的 [SET 選項](../../t-sql/statements/set-statements-transact-sql.md)︰雖然不太可能會用於實際的應用程式中，但若述詞函數的邏輯取決於特定工作階段專屬的  選項且使用者能夠執行任何查詢，則可能導致資訊外漏。 例如，若述詞函數能以隱含方式將字串轉換成 **datetime** ，則可根據目前工作階段的 **SET DATEFORMAT** 選項來篩選不同的資料列。 一般情況下，述詞函數應遵守下列規則︰  
  
-   述詞函數不應以隱含方式將字元字串轉換為以下格式：**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset**，反之亦然，因為這些轉換會受到 [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) 和 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md) 選項影響。 請改用 **CONVERT** 函數，並明確指定樣式參數。  
  
-   述詞函數不應依賴每週第一天的值，因為此值會受到 [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md) 選項影響。  
  
-   述詞函數不應依賴算術或傳回 **NULL** 的彙總運算式，以避免發生錯誤 (例如溢位或除以零)，因為此行為受到 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)、[SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) 及 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md) 選項影響。  
  
-   述詞函數不應比較串連的字串與 **NULL**，因為此行為受到 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md) 選項影響。  
   
  
##  <a name="SecNote"></a> 安全性注意事項：側邊通道攻擊  
 **惡意的安全性原則管理員：** 觀察以下所述十分重要：惡意的安全性原則管理員，具有足夠的權限建立安全性原則上之機密的資料行並有權建立或改變內嵌資料表值函數，可以和另一位使用者共謀，該使用者具有資料表上的選擇權限，可惡意建立設計用來在用戶端通道攻擊推斷資料的內嵌資料表值函數，藉此執行資料竊取。 這類攻擊需要夥伴 (或惡意的使用者授與過多的權限)，並可能需要反覆修改原則 (需要移除述詞的權限，才能中斷結構描述繫結)、修改內嵌資料表值函式、並重複執行目標資料表上的 select 陳述式。 強烈建議在必要時限制權限，並監視任何可疑的活動，例如經常變動的原則和內嵌資料表值函式與資料列層級安全性的相關限制。  
  
 **精巧的查詢：** 很可能透過使用精巧的查詢，導致資訊外洩。 例如， `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` 可讓惡意使用者知道 John Doe 薪資為 $100000。 即使有安全性述詞用來防止惡意使用者直接查詢其他人的薪資，當查詢傳回除以零的例外狀況時，使用者仍可以決定。  
   
  
##  <a name="Limitations"></a> 跨功能的相容性  
 一般情況下，資料列層級安全性將在所有功能下正常運作。 但仍有一些例外狀況。 本節說明搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的特定其他功能使用資料列層級安全性時，數個需要注意的事項及警告。  
  
-   **DBCC SHOW_STATISTICS** 回報關於未篩選資料的統計資料，並可能因此導致洩漏安全性原則所保護的資訊。 有鑑於此，使用者必須擁有資料表，或使用者必須是系統管理員固定伺服器角色、db_owner 固定資料庫角色或 db_ddladmin 固定資料庫角色的成員，才能針對具資料列層級安全性原則的資料表檢視其統計資料物件。  
  
-   **Filestream** RLS 與 Filestream 不相容。  
  
-   **Polybase** RLS 與 Polybase 不相容。  
  
-   **記憶體最佳化資料表**在記憶體最佳化資料表上作為內嵌資料表值函數的安全性述詞必須使用 `WITH NATIVE_COMPILATION` 選項來定義。 使用此選項將會禁止記憶體最佳化資料表不支援的語言功能，並會在建立階段發出適當的錯誤。 如需詳細資訊，請參閱 **記憶體最佳化的資料表簡介** 中的 [記憶體最佳化資料表中的資料列層級安全性](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)一節。  
  
-   **索引檢視表** 一般而言，您可以在檢視上建立安全性原則，並可以在由安全性原則所繫結的資料表上建立檢視。 不過，透過索引的資料列查閱會略過原則，因此您無法在具備安全性原則的資料表上建立索引檢視表。  
  
-   **異動資料擷取**異動資料擷取可能會導致洩漏整個資料列，其中該資料列應篩選至 **db_owner** 的成員，或篩選至啟用資料表的 CDC 時所指定的「控制」角色成員的使用者 (注意︰您可以明確地將這設為 讓所有使用者存取異動資料)。 實際上，**db_owner** 及此控制角色的成員皆可以看到資料表上所有的資料變更，即使資料表上具有安全性原則亦然。  
  
-   **變更追蹤** 變更追蹤可能會導致洩漏資料列的主索引鍵，其中該資料列應同時使用 **SELECT** 及 **VIEW CHANGE TRACKING** 權限篩選至使用者。 實際資料值不會遭到洩漏；僅為資料列的資料行 A 已利用 B 主索引鍵進行更新/插入/刪除。 若主索引鍵包含像是身分證號碼等機密的項目，便會造成問題。 不過，在實務上，此 **CHANGETABLE** 幾乎一律會與原始資料表聯結，以取得最新的資料。  
  
-   **全文檢索搜尋**：由於引進額外聯結以套用資料列層級安全性及避免洩漏應篩選之資料列的主索引鍵，因此使用下列全文檢索搜尋及語意搜尋函數時，應會對查詢的效能造成衝擊︰**CONTAINSTABLE**、semantickeyphrasetable、semanticsimilaritydetailstable、semanticsimilaritytable。  
  
-   **資料行存放區索引**RLS 適用於叢集與非叢集資料行存放區索引。 不過，由於資料列層級安全性套用函數，因此最佳化工具可以在不使用批次模式的情況下修改查詢計劃。  
  
-   **資料分割檢視** Block 述詞不能在資料分割檢視上定義，且不能在使用 Block 述詞的資料表上建立資料分割檢視。 篩選述詞則與資料分割檢視相容。  
  
-   **時態表** 與 RLS 相容。 不過，目前資料表上的安全性述詞不會自動複製到歷程記錄資料表。 若要將安全性原則套用至目前和歷程記錄資料表，您必須個別在每個資料表上新增安全性述詞。  
  
  
##  <a name="CodeExamples"></a> 範例  
  
###  <a name="Typical"></a> A. 向資料庫驗證的使用者案例  
 這個簡短的範例會建立三個使用者、 建立並填入資料表的 6 個資料列，然後建立內嵌資料表值函式和資料表的安全性原則。 此範例示範如何針對不同的使用者篩選 select 陳述式。  
  
 建立三個使用者帳戶，將示範不同的存取功能。  
  
```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```  
  
 建立簡單的資料表來保存資料。  
  
```  
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```  
  
 填入具有 6 個資料列，顯示每個銷售代表的 3 個訂單的資料表。  
  
```  
INSERT Sales VALUES   
(1, 'Sales1', 'Valve', 5),   
(2, 'Sales1', 'Wheel', 2),   
(3, 'Sales1', 'Valve', 4),  
(4, 'Sales2', 'Bracket', 2),   
(5, 'Sales2', 'Wheel', 5),   
(6, 'Sales2', 'Seat', 5);  
-- View the 6 rows in the table  
SELECT * FROM Sales;  
```  
  
 授與讀取權限給每個使用者資料表。  
  
```  
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```  
  
 建立新的結構描述，以及內嵌資料表值函式。 SalesRep 資料行中的資料列相同、且使用者執行查詢時 (`@SalesRep = USER_NAME()`) 或執行查詢的使用者是管理員使用者 (`USER_NAME() = 'Manager'`) 時，此函數會傳回 1。  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result   
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```  
  
 建立依照篩選器述詞中加入函式的安全性原則。 若要啟用此原則，狀態必須設為 ON。  
  
```  
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)   
ON dbo.Sales  
WITH (STATE = ON);  
```  
  
 現在從每個使用者的 Sales 資料表進行選取，藉此測試篩選述詞。  
  
```  
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;   
REVERT;  
```  
  
 管理員應該會看到所有的 6 個資料列。 Sales1 和 Sales2 使用者只能看到他們自己的銷售。  
  
 變更安全性原則，以停用原則。  
  
```  
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```  
  
 現在 Sales1 和 Sales2 使用者可以看到所有的 6 個資料列。  
  
  
###  <a name="MidTier"></a> B. 透過中介層應用程式連接到資料庫的使用者案例  
 此範例示範中介層應用程式如何實作連線篩選，其中應用程式使用者 (或租用戶) 共用相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 (應用程式)。 應用程式在連接到資料庫之後，會在 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) 中設定目前應用程式使用者識別碼，然後安全性原則會明確地篩選此 ID 不應該看到的資料列，並同時避免使用者插入錯誤使用者識別碼的資料列。 不需要任何其他的應用程式變更。  
  
 建立簡單的資料表來保存資料。  
  
```  
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```  
  
 填入具有 6 個資料列，顯示每個應用程式使用者的 3 個訂單的資料表。  
  
```  
INSERT Sales VALUES   
    (1, 1, 'Valve', 5),   
    (2, 1, 'Wheel', 2),   
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),   
    (5, 2, 'Wheel', 5),   
    (6, 2, 'Seat', 5);  
```  
  
 建立應用程式將用來連接的低權限使用者。  
  
```  
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;   
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```  
  
 建立新的結構描述和述詞函式，這將會使用儲存在 **SESSION_CONTEXT** 的應用程式使用者識別碼，以篩選資料列。  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')    
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;   
GO  
```  
  
 建立安全性原則，作為 `Sales`上的篩選述詞及 Block 篩選述詞新增此函數。 由於 **BEFORE UPDATE**及 **BEFORE DELETE** 皆已經過篩選，因此 Block 述詞只需要 **AFTER INSERT** ，且因為先前設定的資料行權限， **資料行無法更新為其他值，所以不需要** AFTER UPDATE `AppUserId` 。  
  
```  
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales AFTER INSERT   
    WITH (STATE = ON);  
```  
  
 在 `Sales` SESSION_CONTEXT **中設定不同的使用者識別碼之後，現在我們可以從**資料表中選取，以模擬連線篩選。 在實務上，開啟連線後，應用程式負責在 **SESSION_CONTEXT** 設定目前的使用者識別碼。  
  
```  
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
--  Note: @read_only prevents the value from changing again   
--  until the connection is closed (returned to the connection pool)  
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;   
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [建立使用者定義函數 &#40;Database Engine&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  
  
