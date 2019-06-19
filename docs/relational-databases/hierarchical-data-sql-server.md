---
title: 階層式資料 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [SQL Server], tables to support
- hierarchyid [Database Engine], concepts
- hierarchical tables [Database Engine]
- SqlHierarchyId
- hierarchyid [Database Engine]
- hierarchical queries [SQL Server], using hierarchyid data type
ms.assetid: 19aefa9a-fbc2-4b22-92cf-67b8bb01671c
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b4cca30125bd6b8fb69893332924d18fbb461cd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706920"
---
# <a name="hierarchical-data-sql-server"></a>階層式資料 (SQL Server)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  內建 **hierarchyid** 資料類型讓儲存與查詢階層式資料更容易。 **hierarchyid** 最適合表示樹狀目錄，這是階層式資料最常見的類型。  
  
 階層式資料的定義為一組資料項目，這些資料項目會依據階層式關聯性，彼此相關。 階層式關聯性表示資料的一個項目是另一個項目的父代。 通常儲存在資料庫的階層式資料範例包含下列：  
  
-   組織結構  
  
-   檔案系統  
  
-   專案中的一組工作  
  
-   語言詞彙的分類表  
  
-   網頁之間的連結圖形  
  
 使用 [hierarchyid](../t-sql/data-types/hierarchyid-data-type-method-reference.md) 做為資料類型來建立具有階層式結構的資料表，或描述儲存在另一個位置的階層式資料結構。 使用 [中的](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06) hierarchyid 函數 [!INCLUDE[tsql](../includes/tsql-md.md)] 來查詢及管理階層式資料。  
  
##  <a name="keyprops"></a> hierarchyid 的主要屬性  
 **hierarchyid** 資料類型的值代表樹狀目錄階層中的位置。 **hierarchyid** 的值具有下列屬性：  
  
-   極度壓縮  
  
     代表樹狀目錄 (含有 *n* 個節點) 中之節點所需的平均位元數目會因平均扇出 (節點子系的平均數目) 而不同。 若為小型扇出 (0-7)，其大小大約是 6\*logA*n* 個位元，其中 A 是平均扇出。 在平均 fanout 為 6 個階層之 100,000 人員的組織階層中，節點會佔用大約 38 位元。 然後，這會四捨五入成 40 位元 (或 5 個位元組)，以便進行儲存。  
  
-   比較是按照深度優先順序  
  
     假設有兩個 **hierarchyid** 值 (**a** 和 **b**)，**a<b** 就表示在樹狀目錄的深度優先周遊中，a 在 b 前面。 **hierarchyid** 資料類型的索引採用深度優先順序，而且在深度優先周遊中彼此接近的節點會以彼此接近的方式儲存。 例如，某筆記錄的子系會儲存在該記錄旁。  
  
-   支援任意插入和刪除  
  
     透過使用 [GetDescendant](../t-sql/data-types/getdescendant-database-engine.md) 方法，您就一定能夠在任何指定節點的右側、任何指定節點的左側，或任何兩個同層級之間產生同層級。 在階層中插入或刪除任意的節點數目時，比較屬性會保留下來。 大部分的插入和刪除項目都會保留壓縮度屬性。 不過，兩個節點之間的插入項目則會以稍微少的壓縮表示來產生 hierarchyid 值。  
  
  
##  <a name="limits"></a> hierarchyid 的限制  
 **hierarchyid** 資料類型具有下列限制：  
  
-   **hierarchyid** 類型的資料行不會自動代表樹狀目錄。 應用程式負責決定是否要產生並指派 **hierarchyid** 值，以便讓資料列之間所需的關聯性反映在值中。 有些應用程式可能有 **hierarchyid** 類型的資料行，表示在另一個資料表中定義之階層的位置。  
  
-   應用程式負責管理產生與指派 **hierarchyid** 值的並行。 除非應用程式使用唯一索引鍵條件約束或透過自己的邏輯強制本身的唯一性，否則，不保證資料行中的 **hierarchyid** 值是唯一的。  
  
-   由 **hierarchyid** 值代表的階層式關聯性不會像外部索引鍵關聯性般強制執行。 如果 A 擁有子系 B，然後刪除 A 留下 B，讓關聯性變成不存在的記錄，這種階層式關聯性是可能發生而且有時候是恰當的。 如果無法接受這種行為，應用程式必須在刪除父系前，查詢下階。  
  
  
##  <a name="alternatives"></a> 使用 hierarchyid 替代選項的時機  
 代表階層式資料的兩個 **hierarchyid** 替代選項為：  
  
-   父子式  
  
-   XML  
  
 **hierarchyid** 通常優先於這些替代選項。 但是，以下詳述替代選項可能優先於 hierarchyid 的特定情況。  
  
### <a name="parentchild"></a>父子式  
 使用父子式方式時，每個資料列都包含一個父系的參考。 下表定義在父子關聯性中包含父系和子系資料列時所使用的一般資料表：  
  
```sql
USE AdventureWorks2012 ;  
GO  
  
CREATE TABLE ParentChildOrg  
   (  
    BusinessEntityID int PRIMARY KEY,  
    ManagerId int REFERENCES ParentChildOrg(BusinessEntityID),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
```  
  
 比較父子式和 **hierarchyid** 的一般作業  
  
-   使用 **hierarchyid**進行子樹查詢時，速度明顯加快。  
  
-   而使用 **hierarchyid**進行直接下階查詢時，速度則稍慢。  
  
-   使用 **hierarchyid**移動非分葉節點時，速度比較慢。  
  
-   使用 **hierarchyid**插入非分葉節點與插入或移動分葉節點時，其複雜程度相同。  
  
 下列狀況存在時，最好使用父子式：  
  
-   索引鍵的大小很重要。 如果節點數目相同， **hierarchyid** 值會等於或大於整數系列 (**smallint**、 **int**、 **bigint**) 值。 在極少的情況下，這是使用 [父子式] 的唯一原因，因為比起使用 [父子式] 結構時所需要的通用資料表運算式， **hierarchyid** 的 I/O 位置明顯較好，而且 CPU 的複雜性較高。  
  
-   查詢很少會查詢整個階層的區段。 換句話說，查詢通常只處理階層中的單一點。 在這些情況下，共同位置就不重要。 例如，如果組織資料表僅用於處理個別員工的薪資，最好使用 [父子式]。  
  
-   非分葉的子樹會經常移動，因此效能非常重要。 在父子式表示中，變更資料列在階層中的位置會影響單一資料列。 在 **hierarchyid** 使用方式中變更資料列的位置會影響 *n* 個資料列，其中 *n* 是要移動之樹狀子目錄中的節點數目。  
  
     如果非分葉子樹經常移動且效能非常重要，但是大部分的移動都是在定義良好的階層層級進行時，請考慮將較高和較低的層級分割為兩個階層。 這樣會全部移到較高階層的分葉層級中。 例如，請考慮由服務主控之網站的階層。 網站包含許多以階層方式排列的頁面。 主控的網站可能會移到網站階層的其他位置，但是從屬的頁面很少會重新排列。 這可能會透過下列方式表示：  
  
    ```sql
    CREATE TABLE HostedSites   
       (  
        SiteId hierarchyid, PageId hierarchyid  
       ) ;  
    GO  
    ```  
  
  
### <a name="xml"></a>XML  
 XML 文件是一個樹狀結構，因此，單一的 XML 資料類型執行個體可以代表一個完整的階層。 In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] when an XML hierarchyid 函數dex is created, **hierarchyid** values are used hierarchyid 函數ternally to represent the position hierarchyid 函數 the hierarchy.  
  
 如果以下所有狀況成立，使用 XML 資料類型可能比較好：  
  
-   永遠會儲存與擷取完整的階層。  
  
-   應用程式使用的資料為 XML 格式。  
  
-   述詞搜尋會受到相當的限制，而且效能並不重要。  
  
 例如，如果應用程式追蹤多個組織，務必儲存與擷取完整的組織階層，而且不要在單一組織中查詢，下列表單的資料表才可能有意義：  
  
```sql
CREATE TABLE XMLOrg   
    (  
    Orgid int,  
    Orgdata xml  
    ) ;  
GO  
```  
  
  
##  <a name="indexing"></a> 階層式資料的索引策略  
 編製階層式資料索引有兩種策略：  
  
-   **深度優先**  
  
     如果是深度優先的索引，會將子樹中的資料列儲存在彼此的附近。 例如，透過某位經理管理的所有員工都會儲存在經理記錄的附近。  
  
     在深度優先的索引中，節點子樹的所有節點都會位於相同位置。 因此，深度優先的索引在回應關於子樹的查詢 (例如，「尋找此資料夾及其子資料夾中的所有檔案」) 時很有效率。  
  
-   **廣度優先**  
  
     如果是廣度優先，會將資料列與階層的每個層級儲存在一起。 例如，直接由相同經理管理之員工的記錄會儲存在彼此的附近。  
  
     在廣度優先的索引中，節點的所有直接子系都會位於相同位置。 因此，廣度優先的索引在回應關於下層子系的查詢 (例如，「尋找直接回報給此經理的所有員工」) 時很有效率。  
  
 不論是讓深度優先、廣度優先，或是兩者，還是那個要產生叢集索引鍵 (如果有的話)，都取決於上述查詢類型的相對重要性，以及 SELECT 和DML 作業的相對重要性。 如需索引策略的詳細範例，請參閱[教學課程：使用 hierarchyid 資料類型](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)。  
  
  
### <a name="creating-indexes"></a>建立索引  
 GetLevel() 方法可以用來建立廣度優先排序。 在下列範例中，會同時建立廣度優先和深度優先的索引：  
  
```sql
USE AdventureWorks2012 ;   -- wmimof
GO  
  
CREATE TABLE Organization  
   (  
    BusinessEntityID hierarchyid,  
    OrgLevel as BusinessEntityID.GetLevel(),   
    EmployeeName nvarchar(50) NOT NULL  
   ) ;  
GO  
  
CREATE CLUSTERED INDEX Org_Breadth_First   
    ON Organization(OrgLevel,BusinessEntityID) ;  
GO  
  
CREATE UNIQUE INDEX Org_Depth_First   
    ON Organization(BusinessEntityID) ;  
GO  
```  
  
  
## <a name="examples"></a>範例  
  
### <a name="simple-example"></a>簡單範例  
 下列範例有意經過簡化以協助您開始使用。 首先，建立資料表以保留一些地理資料。  
  
```sql
CREATE TABLE SimpleDemo  
(
    Level hierarchyid NOT NULL,  
    Location nvarchar(30) NOT NULL,  
    LocationType nvarchar(9) NULL
);
```  
  
 現在，插入一些大陸、國家/地區、州和城市的資料。  
  
```sql
INSERT SimpleDemo  
    VALUES   
('/1/', 'Europe', 'Continent'),  
('/2/', 'South America', 'Continent'),  
('/1/1/', 'France', 'Country'),  
('/1/1/1/', 'Paris', 'City'),  
('/1/2/1/', 'Madrid', 'City'),  
('/1/2/', 'Spain', 'Country'),  
('/3/', 'Antarctica', 'Continent'),  
('/2/1/', 'Brazil', 'Country'),  
('/2/1/1/', 'Brasilia', 'City'),  
('/2/1/2/', 'Bahia', 'State'),  
('/2/1/2/1/', 'Salvador', 'City'),  
('/3/1/', 'McMurdo Station', 'City');  
```  
  
 選取資料，並加入資料行以將層級資料轉換為容易了解的文字值。 此查詢也會依 **hierarchyid** 資料類型來排序結果。  
  
```sql
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], *   
    FROM SimpleDemo ORDER BY Level;  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
Converted Level  Level     Location         LocationType  
/1/              0x58      Europe           Continent  
/1/1/            0x5AC0    France           Country  
/1/1/1/          0x5AD6    Paris            City  
/1/2/            0x5B40    Spain            Country  
/1/2/1/          0x5B56    Madrid           City  
/2/              0x68      South America    Continent  
/2/1/            0x6AC0    Brazil           Country  
/2/1/1/          0x6AD6    Brasilia         City  
/2/1/2/          0x6ADA    Bahia            State  
/2/1/2/1/        0x6ADAB0  Salvador         City  
/3/              0x78      Antarctica       Continent  
/3/1/            0x7AC0    McMurdo Station  City  
```  
  
 請注意，即使階層內部不一致，仍具有有效的結構。 Bahia 是唯一的州。 它會在階層中以 Brasilia 城市的同層級顯示。 同樣地，McMurdo Station 沒有父國家/地區。 使用者必須決定此階層類型是否適用。  
  
 加入另一個資料列並選取結果。  
  
```sql
INSERT SimpleDemo  
    VALUES ('/1/3/1/', 'Kyoto', 'City'), ('/1/3/1/', 'London', 'City');  
SELECT CAST(Level AS nvarchar(100)) AS [Converted Level], * FROM SimpleDemo ORDER BY Level;  
```  
  
 這會顯示更多可能的問題。 Kyoto 可插入為層級 `/1/3/1/` ，但卻沒有父層級 `/1/3/`。 而 London 和 Kyoto 的 **hierarchyid**值相同。 同樣地，使用者必須決定此階層類型是否適用，並封鎖不適用的值。  
  
 此外，此資料表未使用階層 `'/'`的頂端。 由於所有大陸沒有共同的父系，因此已省略。 您可以加入整個地球，以加入一個父系。  
  
```sql
INSERT SimpleDemo  
    VALUES ('/', 'Earth', 'Planet');  
```  
  
##  <a name="tasks"></a> 相關工作  
  
###  <a name="migrating"></a> 從父子式移轉到 hierarchyid  
 大部分的樹狀目錄都是使用 [父子式] 代表。 從 [父子式] 結構遷移到使用 **hierarchyid** 的資料表最簡單的方式，就是使用暫存資料行或暫存資料表來追蹤每個階層層級的節點數。 如需移轉父子式資料表的範例，請參閱[教學課程：使用 hierarchyid 資料類型](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)的第 1 課。  
  
  
###  <a name="BKMK_ManagingTrees"></a> 使用 hierarchyid 管理樹狀結構  
 雖然 **hierarchyid** 資料行不需要代表樹狀結構，但是應用程式可以輕易地確認這就是樹狀結構。  
  
-   產生新值時，請執行下列其中之一：  
  
    -   追蹤父資料列中的最後一個子系號碼。  
  
    -   計算最後一個子系。 若要有效率地執行這個動作，需要使用廣度優先索引。  
  
-   在資料行上建立唯一的索引 (也許是叢集索引鍵的一部份) 以強制執行唯一性。 若要確保插入唯一的值，請執行下列其中之一：  
  
    -   偵測唯一的索引鍵違規失敗，然後重試。  
  
    -   判斷每個新子節點的唯一性，然後插入該子節點做為可序列化交易的一部分。  
  
  
#### <a name="example-using-error-detection"></a>使用錯誤偵測的範例  
 在下列範例中，範例程式碼會計算新子系的 **EmployeeId** 值，然後偵測任何索引鍵違規，並傳回 **INS_EMP** 標記，以便為新的資料列重新計算 **EmployeeId** 值：  
  
```sql
USE AdventureWorks ;  
GO  
  
CREATE TABLE Org_T1  
   (  
    EmployeeId hierarchyid PRIMARY KEY,  
    OrgLevel AS EmployeeId.GetLevel(),  
    EmployeeName nvarchar(50)   
   ) ;  
GO  
  
CREATE INDEX Org_BreadthFirst ON Org_T1(OrgLevel, EmployeeId);
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50) )   
AS  
BEGIN  
    DECLARE @last_child hierarchyid;
INS_EMP:   
    SELECT @last_child = MAX(EmployeeId) FROM Org_T1   
        WHERE EmployeeId.GetAncestor(1) = @mgrid;
    INSERT INTO Org_T1 (EmployeeId, EmployeeName)  
        SELECT @mgrid.GetDescendant(@last_child, NULL), @EmpName;
-- On error, return to INS_EMP to recompute @last_child  
IF @@error <> 0 GOTO INS_EMP   
END ;  
GO  
```  
  
  
#### <a name="example-using-a-serializable-transaction"></a>使用序列化交易的範例  
 **Org_BreadthFirst** 索引可確定判斷 **@last_child** 會使用範圍搜尋。 除了應用程式可能想要檢查的其他錯誤情況之外，插入後的重複索引鍵違規會指出新增多個具有相同識別碼之員工的嘗試，因此必須重新計算 **@last_child** 。 下列程式碼使用序列化交易與廣度優先索引來計算新的節點值：  
  
```sql
CREATE TABLE Org_T2  
    (  
    EmployeeId hierarchyid PRIMARY KEY,  
    LastChild hierarchyid,   
    EmployeeName nvarchar(50)   
    ) ;  
GO  
  
CREATE PROCEDURE AddEmp(@mgrid hierarchyid, @EmpName nvarchar(50))   
AS  
BEGIN  
DECLARE @last_child hierarchyid  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION   
  
UPDATE Org_T2   
SET @last_child = LastChild = EmployeeId.GetDescendant(LastChild,NULL)  
WHERE EmployeeId = @mgrid  
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(@last_child, @EmpName)  
COMMIT  
END ;  
```  
  
 下列程式碼會使用三個資料列擴展資料表，然後傳回結果：  
  
```sql
INSERT Org_T2 (EmployeeId, EmployeeName)   
    VALUES(hierarchyid::GetRoot(), 'David') ;  
GO  
AddEmp 0x , 'Sariya'  
GO  
AddEmp 0x58 , 'Mary'  
GO  
SELECT * FROM Org_T2  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
```  
EmployeeId LastChild EmployeeName  
---------- --------- ------------  
0x        0x58       David  
0x58      0x5AC0     Sariya  
0x5AC0    NULL       Mary  
```  
  
  
###  <a name="BKMK_EnforcingTrees"></a> 強制執行樹狀結構  
 以上的範例說明應用程式可以如何確保樹狀結構的維護。 若要透過條件約束強制執行樹狀結構，定義每個節點之父系的計算資料行可以使用傳回主要索引鍵識別碼的外部索引鍵條件約束建立。  
  
```sql
CREATE TABLE Org_T3  
(  
   EmployeeId hierarchyid PRIMARY KEY,  
   ParentId AS EmployeeId.GetAncestor(1) PERSISTED    
      REFERENCES Org_T3(EmployeeId),  
   LastChild hierarchyid,   
   EmployeeName nvarchar(50)  
)  
GO  
```  
  
 不信任可以維護階層式樹狀結構的程式碼具有資料表的 DML 直接存取權時，最好使用這個方法強制關聯性。 不過，由於必須針對每個 DML 作業檢查條件約束，這個方法可能會降低效能。  
  
  
###  <a name="findclr"></a> 透過使用 CLR 尋找上階  
 與階層中兩個節點相關的常見作業就是尋找最低通用上階。 這可以寫入 [!INCLUDE[tsql](../includes/tsql-md.md)] 或 CLR，因為這兩者都可以使用 **hierarchyid** 類型。 因為效能將會更快，因此建議使用 CLR。  
  
 使用下列的 CLR 程式碼，列出上階並尋找最低通用上階：  
  
```csharp
using System;  
using System.Collections;  
using System.Text;  
using Microsoft.SqlServer.Server;  // SqlFunction Attribute
using Microsoft.SqlServer.Types;   // SqlHierarchyId
  
public partial class HierarchyId_Operations  
{  
    [SqlFunction(FillRowMethodName = "FillRow_ListAncestors")]
    public static IEnumerable ListAncestors(SqlHierarchyId h)
    {  
        while (!h.IsNull)  
        {  
            yield return (h);  
            h = h.GetAncestor(1);  
        }  
    }  
    public static void FillRow_ListAncestors(
        Object obj,
        out SqlHierarchyId ancestor
        )
    {  
        ancestor = (SqlHierarchyId)obj;  
    }  
  
    public static HierarchyId CommonAncestor(
        SqlHierarchyId h1,
        HierarchyId h2
        )  
    {  
        while (!h1.IsDescendantOf(h2))  
            h1 = h1.GetAncestor(1);  
  
        return h1;  
    }  
}  
```  
  
 若要在下列 **範例中使用** ListAncestor **和** CommonAncestor [!INCLUDE[tsql](../includes/tsql-md.md)] 方法執行類似如下的程式碼，請在 **中建置 DLL 並建立** HierarchyId_Operations [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組件：  
  
```sql
CREATE ASSEMBLY HierarchyId_Operations   
    FROM '<path to DLL>\ListAncestors.dll';
GO  
```  
  
  
###  <a name="ancestors"></a> 列出上階  
 建立節點上階清單是一個常見的作業，例如，在組織中顯示位置。 其中一個方法是，利用以上定義的 **HierarchyId_Operations** 類別，使用資料表值函數：  
  
 使用 [!INCLUDE[tsql](../includes/tsql-md.md)]：  
  
```sql
CREATE FUNCTION ListAncestors (@node hierarchyid)  
RETURNS TABLE (node hierarchyid)  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.ListAncestors  
GO  
```  
  
 使用範例：  
  
```sql
DECLARE @h hierarchyid  
SELECT @h = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0' -- /1/1/5/2/  
  
SELECT LoginID, OrgNode.ToString() AS LogicalNode  
FROM HumanResources.EmployeeDemo AS ED  
JOIN ListAncestors(@h) AS A   
   ON ED.OrgNode = A.Node  
GO  
```  
  
  
###  <a name="lowestcommon"></a> 尋找最低通用上階  
 使用以上定義的 **HierarchyId_Operations** 類別建立下列的 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數，尋找與階層中兩個節點相關的最低通用上階：  
  
```sql
CREATE FUNCTION CommonAncestor (@node1 hierarchyid, @node2 hierarchyid)  
RETURNS hierarchyid  
AS  
EXTERNAL NAME HierarchyId_Operations.HierarchyId_Operations.CommonAncestor  
GO  
```  
  
 使用範例：  
  
```sql
DECLARE @h1 hierarchyid, @h2 hierarchyid;
  
SELECT @h1 = OrgNode   
FROM  HumanResources.EmployeeDemo   
WHERE LoginID = 'adventure-works\jossef0'; -- Node is /1/1/3/  
  
SELECT @h2 = OrgNode   
FROM HumanResources.EmployeeDemo    
WHERE LoginID = 'adventure-works\janice0'; -- Node is /1/1/5/2/  
  
SELECT OrgNode.ToString() AS LogicalNode, LoginID   
FROM HumanResources.EmployeeDemo    
WHERE OrgNode = dbo.CommonAncestor(@h1, @h2) ;  
```  
  
 產生的節點是 /1/1/  
  
  
###  <a name="BKMK_MovingSubtrees"></a> 移動子樹  
 另一個常見的作業是移動子樹。 以下的程序使用 **@oldMgr** 的樹狀子目錄，並讓其 (包括 **@oldMgr** ) 成為 **@newMgr** 進行子樹查詢時，速度明顯加快。  
  
```sql
CREATE PROCEDURE MoveOrg(@oldMgr nvarchar(256), @newMgr nvarchar(256) )  
AS  
BEGIN  
DECLARE @nold hierarchyid, @nnew hierarchyid  
SELECT @nold = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @oldMgr ;  
  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
BEGIN TRANSACTION  
SELECT @nnew = OrgNode FROM HumanResources.EmployeeDemo WHERE LoginID = @newMgr ;  
  
SELECT @nnew = @nnew.GetDescendant(max(OrgNode), NULL)   
FROM HumanResources.EmployeeDemo WHERE OrgNode.GetAncestor(1)=@nnew ;  
  
UPDATE HumanResources.EmployeeDemo    
SET OrgNode = OrgNode.GetReparentedValue(@nold, @nnew)  
WHERE OrgNode.IsDescendantOf(@nold) = 1 ;  
  
COMMIT TRANSACTION;
END ;  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [Hierarchyid 資料類型方法參考](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)   
 [教學課程：使用 hierarchyid 資料類型](../relational-databases/tables/tutorial-using-the-hierarchyid-data-type.md)   
 [hierarchyid &#40;Transact-SQL&#41;](../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
  
