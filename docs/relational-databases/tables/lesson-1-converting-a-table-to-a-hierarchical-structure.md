---
title: 第 1 課：將資料表轉換為階層式結構 | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14b490c48cf60c01efa1a0c3fed38b4aabb10495
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716283"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>第 1 課：將資料表轉換為階層式結構
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
具有使用自我聯結表達階層式關聯性之資料表的客戶可以使用本課程當做指導方針，將其資料表轉換為階層式結構。 從這種表示法移轉到另一種使用 **hierarchyid**之表示法的步驟非常簡單。 移轉之後，使用者將會有一個精簡而且容易了解的階層式表示法，可以使用數種方式建立索引以便進行有效率的查詢。  
  
本課程會檢查現有的資料表、建立包含 **hierarchyid** 資料行的新資料列、使用來源資料表中的資料擴展資料表，然後示範三個索引策略。 這個課程包含下列主題：  
 
  
## <a name="prerequisites"></a>Prerequisites  
若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2017 sample databases](https://docs.microsoft.com/sql/samples/adventureworks-install-configure) (AdventureWorks2017 範例資料庫)。

如需在 SSMS 中還原資料庫的指示，請參閱：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。  

## <a name="examine-the-current-structure-of-the-employee-table"></a>檢查 Employee 資料表的目前結構
範例 AdventureWorks2017 (或更新版本) 資料庫在 **HumanResources** 結構描述中包含一個 **Employee** 資料表。 為避免變更原始資料表，此步驟會製作一個名為 **EmployeeDemo** 的 **Employee**資料表複本。 若要簡化範例，您僅能從原始資料表複製五個資料行。 然後，您可以查詢 **HumanResources.EmployeeDemo** 資料表，以便在不使用 **hierarchyid** 資料類型的情況下，檢閱如何將資料表中的資料結構化。  
  
### <a name="copy-the-employee-table"></a>複製 Employee 資料表  
  
1.  在 [查詢編輯器] 視窗中執行下列程式碼，以便將資料表結構和資料從 **Employee** 資料表複製到名稱為 **EmployeeDemo**的新資料表。 由於原始的資料表已經使用 hierarchyid，此查詢基本上會使階層扁平化，以擷取員工的經理。 在本課程的後續部分中，我們將會重建此階層。

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]


   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>檢查 EmployeeDemo 資料表的結構和資料  
  
-   這個新的 **EmployeeDemo** 資料表代表現有的資料庫中，您想要移轉成新結構的一般資料表。 在 [查詢編輯器] 視窗中，執行下列程式碼以顯示資料表如何使用自我聯結來顯示員工/主管關聯性：  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    會繼續顯示結果，總共包含 290 個資料列。  
  
請注意， **ORDER BY** 子句會使輸出將每個管理階層的直屬員工列在一起。 例如，**MgrID** 1 (ken0) 的全部七個直屬員工會緊接著彼此列出。 雖然並非不可能，但是要將最終回報給 **MgrID** 1 的所有人員群組在一起更為困難。  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>使用現有的階層式資料填入資料表
此工作會建立一個新的資料表，並以 **EmployeeDemo** 資料表中的資料填入該資料表。 此工作的步驟如下：  
  
-   建立包含 **hierarchyid** 資料行的新資料表。 此資料行可以取代現有的 **EmployeeID** 和 **ManagerID** 資料行。 不過，您將會保留這些資料行。 這是因為現有的應用程式可能會參考這些資料行，而且這些資料行也可以在轉換後，協助您了解資料。 資料表定義指定 **OrgNode** 為主索引鍵，其會要求該資料行所包含的值不得重複。 **OrgNode** 資料行上的叢集索引將以 **OrgNode** 順序儲存資料。    
-   建立暫存資料表，該資料表可用於追蹤各個主管手下的直屬員工人數。 
-   使用 **EmployeeDemo** 資料表中的資料，填入新資料表。  
  
### <a name="to-create-a-new-table-named-neworg"></a>若要建立名稱為 NewOrg 的新資料表  
  
-   在 [查詢編輯器] 視窗中，執行下列程式碼以建立名稱為 **HumanResources.NewOrg**的新資料表：  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="create-a-temporary-table-named-children"></a>建立名為 #Children 的暫存資料表  
  
1.  建立名為 **#Children** 的暫存資料表，以及名稱為 **Num** 的資料行，該資料行將包含每個節點的子系數目：  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  新增索引以大幅提高填入 **NewOrg** 資料表的查詢速度：  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>填入 NewOrg 資料表  
  
1.  遞迴查詢禁止包含彙總的子查詢。 反之，會使用下列程式碼填入 **#Children** 資料表；該程式碼是使用 [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) 方法填入 **Num** 資料行：  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  檢閱 **#Children** 資料表。 請注意 **Num** 資料行如何包含每個主管的序號。  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  填入 **NewOrg** 資料表。 使用 GetRoot 和 ToString 方法，將 **Num** 值串連到 **hierarchyid** 格式，然後以產生的階層式值更新 **OrgNode** 資料行：  
  
    ```sql  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   

    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  將 **hierarchyid** 資料行轉換為字元格式時，會比較容易了解該資料行。 執行下列程式碼 (其中包含 **OrgNode** 資料行之兩種表示法)，以檢閱 **NewOrg** 資料表中的資料：  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    **LogicalNode** 資料行會將 **hierarchyid** 資料行轉換為更容易讀取之代表階層的文字格式。 在其餘工作中，您將使用 `ToString()` 方法，顯示 **hierarchyid** 資料行的邏輯格式。  
  
5.  卸除不再需要的暫存資料表：  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>最佳化 NewOrg 資料表
您在[使用現有的階層式資料填入資料表](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)工作中建立的 **NewOrd** 資料表包含所有員工資訊，並使用 **hierarchyid** 資料類型代表階層式結構。 此工作會新增索引以支援在 **hierarchyid** 資料行上進行搜尋。  
  

**hierarchyid** 資料行 (**OrgNode**) 是 **NewOrg** 資料表的主要索引鍵。 建立資料表時，它包含名為 **PK_NewOrg_OrgNode** 的叢集索引以強制 **OrgNode** 資料行的唯一性。 此叢集索引也支援深度優先的資料表搜尋。  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>建立 NewOrg 資料表的索引以便進行有效率的搜尋  
  
1.  為協助在階層的相同層級進行查詢，使用 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 方法來建立階層中包含層級的計算資料行。 然後，在層級和 **Hierarchyid**上建立複合式索引。 執行下列程式碼以建立計算資料行和廣度優先的索引：  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  在 **EmployeeID** 資料行上建立唯一的索引。 這是依 **EmployeeID** 號碼之單一員工的傳統單一查閱。 執行下列程式碼，在 **EmployeeID**上建立索引：  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  執行下列程式碼，以全部三個索引的順序，從資料表擷取資料：  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  比較結果集以查看每個索引類型中儲存的順序。 只有每個輸出的前四個資料列遵照這個順序。  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    深度優先索引：員工記錄緊接著其主管儲存。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    **EmployeeID**-優先索引：資料列會以 **EmployeeID** 順序儲存。  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> 如需顯示深度優先索引與廣度優先索引間差異的圖表，請參閱[階層式資料 &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)。  
  
### <a name="drop-the-unnecessary-columns"></a>卸除不必要的資料行  
  
1.  **ManagerID** 資料行代表員工/主管的關聯性，此種關聯性現在以 **OrgNode** 資料行代表。 如果其他應用程式不需要 **ManagerID** 資料行，請考慮使用下列陳述式卸除該資料行：  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  **EmployeeID** 資料行也是多餘的。 **OrgNode** 資料行可唯一識別每個員工。 如果其他應用程式不需要 **EmployeeID** 資料行，請考慮使用下列程式碼先卸除索引，再卸除該資料行：  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>以新的資料表取代原始資料表  
  
1.  如果您的原始資料表包含任何額外的索引或條件約束，請將它們新增到 **NewOrg** 資料表中。  
  
2.  以新的資料表取代舊的 **EmployeeDemo** 資料表。 執行下列程式碼卸除舊的資料表，然後以舊名稱重新命名新的資料表：  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  執行下列程式碼檢查最終的資料表：  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>後續步驟
下一篇文章教導您如何在階層式資料表中建立和管理資料。 

請前往下一篇文章以深入了解：
> [!div class="nextstepaction"]
> [後續步驟](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)
