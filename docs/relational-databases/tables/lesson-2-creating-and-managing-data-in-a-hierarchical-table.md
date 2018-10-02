---
title: 第 2 課：在階層式資料表中建立與管理資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54a3323e550ba3534fdc491e42c70c43ba686dc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782046"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>第 2 課：在階層式資料表中建立與管理資料
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
在第 1 課中，您修改了現有的資料表以使用 **hierarchyid** 資料類型，並使用現有資料的表示法來擴展 **hierarchyid** 資料行。 在本課程中，您將從新資料表開始，然後使用階層式方法插入資料。 接著，您將使用階層式方法來查詢與操作資料。 

## <a name="prerequisites"></a>Prerequisites  
若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2017 sample databases](https://docs.microsoft.com/sql/samples/adventureworks-install-configure) (AdventureWorks2017 範例資料庫)。

如需在 SSMS 中還原資料庫的指示，請參閱：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>使用 hierarchyid 資料類型建立資料表
以下範例會建立名稱為 EmployeeOrg 的資料表，其中同時包含員工資料及其回報的階層。 本範例會在 AdventureWorks2017 資料庫中建立資料表，但這是選擇性的。 為了要維持此範例的簡單性，此資料表僅包含五個資料行：  
  
-   OrgNode 是一個 **hierarchyid** 資料行，其中儲存階層式關聯性。   
-   OrgLevel 是一個以 OrgNode 資料行為基礎的計算資料行，後者可將每個節點層級儲存在階層中。 它將會用於廣度優先的索引。  
-   EmployeeID 包含用於應用程式 (例如，薪資) 的一般員工識別碼。 在開發新應用程式時，這些應用程式可以使用 OrgNode 資料行，因此不需要另外的這個 EmployeeID 資料行。   
-   EmpName 包含員工的名稱。    
-   Title 包含員工的職稱。  

## <a name="create-the-employeeorg-table"></a>建立 EmployeeOrg 資料表  
  
1.  在 [查詢編輯器] 視窗中，執行下列程式碼來建立 `EmployeeOrg` 資料表。 指定 `OrgNode` 資料行做為具有叢集索引的主要索引鍵將會建立深度優先的索引：  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  執行下列程式碼，在 `OrgLevel` 和 `OrgNode` 資料行上建立複合式索引，以支援有效的廣度優先搜尋：  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
資料表現在已經準備好可以填寫資料。 下一個工作將是使用階層式方法擴展資料表。   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>使用階層式方法填入階層式資料表
AdventureWorks2017 行銷部門有 8 名員工。 員工層級如下：  
  
**David**( **EmployeeID** 6) 是行銷經理。 **David**管理三名行銷專員：  
  
-   **Sariya**( **EmployeeID** 46)  
  
-   **John**( **EmployeeID** 271)  
  
-   **Jill**( **EmployeeID** 119)  
  
**Sariya** 管理行銷助理**Wanida** ( **EmployeeID**269)， **John** 管理行銷助理**Mary** ( **EmployeeID**272)。  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>插入階層樹狀結構的根目錄  
  
1.  下列範例會將行銷經理 **David** 插入階層根目錄的資料表中。 **OrdLevel** 資料行為計算資料行。 因此，不是 INSERT 陳述式的一部分。 第一筆記錄使用 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 方法，將這個第一筆記錄擴展為階層的根目錄。  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  執行下列節點以檢查資料表中的初始資料列：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
如同上一個課程，我們使用 `ToString()` 方法，將 **hierarchyid** 資料類型轉換為比較容易了解的格式。  
  
### <a name="insert-a-subordinate-employee"></a>插入從屬員工  
  
1.  **David** 管理 **Sariya**。 若要插入 **Sariya** 的節點，您必須建立適合 **hierarchyid** 資料類型的 **OrgNode**值。 下列程式碼會建立 **hierarchyid** 資料類型的變數，並使用資料表的 OrgNode 根目錄值擴展。 然後，搭配 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 方法使用該變數來插入從屬節點的資料列。 `GetDescendant` 會採用兩個引數。 檢閱下列引數值的選項：  
  
    -   如果父系為 NULL， `GetDescendant` 會傳回 NULL。  
    -   如果父系不是 NULL，而 child1 和 child2 都是 NULL， `GetDescendant` 則會傳回父系的一個子系。  
    -   如果父系和 child1 都不是 NULL，而 child2 是 NULL， `GetDescendant` 會傳回父系中大於 child1 的子系。   
    -   如果父系和 child2 不是 NULL，而 child1 是 NULL， `GetDescendant` 會傳回父系中小於 child2 的子系。   
    -   如果父系、child1 和 child2 都不是 NULL， `GetDescendant` 會傳回父系中大於 child1 且小於 child2 的子系。  
  
    下列程式碼使用根目錄父系的 `(NULL, NULL)` 引數，因為除了根目錄之外，資料表中還沒有任何資料列。 執行下列程式碼以插入 **Sariya**：  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  從第一個程序開始重複查詢，以查詢資料表並查看項目如何出現：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>建立輸入新節點的程序  
  
1.  若要簡化輸入資料的方式，請建立下列預存程序，將員工新增到 **EmployeeOrg** 資料表中。 該程序會接受要新增之員工的輸入值。 這包括新員工之主管的 **EmployeeID** 、新員工的 **EmployeeID** 號碼，及其姓氏和職稱。 此程序會使用 `GetDescendant()` 以及 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 方法。 執行下列程式碼以建立程序：  
  
    ```sql  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  下列範例會加入 **David**直接或間接管理的其餘 4 名員工。  
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  再次執行下列查詢，檢查 **EmployeeOrg** 資料表中的資料列：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    /1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
資料表現在已經完全擴展到行銷組織了。  

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>使用階層方法查詢階層式資料表
既然 HumanResources.EmployeeOrg 資料表會完全擴展，此工作將會顯示如何使用某些階層式方法查詢階層。  
  
### <a name="find-subordinate-nodes"></a>尋找從屬節點  
  
1.  Sariya 有一個從屬員工。 若要查詢 Sariya 的部屬，請執行使用 [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) 方法的下列查詢：  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    結果會同時列出 Sariya 和 Wanida。 Sariya 是層級 0 的下階，因此會被列出。 Wanida 是層級 1 的下階。  
  
2.  您也可以使用 [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) 方法來查詢這項資訊。 `GetAncestor` 會針對您嘗試傳回的層級傳回一個引數。 由於 Wanida 是 Sariya 下的一個層級，請按照下列程式碼的示範，使用 `GetAncestor(1)` ：  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    這次結果列出只 Wanida。  
  
3.  現在，將 `@CurrentEmployee` 變更為 David (EmployeeID 6)，並將層級變更為 2。 執行下列程式碼也可以傳回 Wanida：  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    這次，您也可以接收到兩個層級下的 Mary，她也是回報給 David。  
  
## <a name="use-getroot-and-getlevel"></a>使用 GetRoot 與 GetLevel  
  
1.  階層成長得越大時，判斷成員在階層中的位置時，也就變得更加困難。 使用 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 方法，尋找階層中，每個資料列下有多少層級。 執行下列程式碼以檢視所有資料列的層級：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  使用 [GetRoot](../../t-sql/data-types/getroot-database-engine.md) 方法，尋找階層中的根節點。 下列程式碼範例會傳回根目錄的單一資料列：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>使用階層式方法重新排列階層式資料表中的資料順序
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
重新組織階層是常見的維護工作。 在這項工作中，我們將會使用 UPDATE 陳述式搭配 [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) 方法，先將單一資料列移到階層中的新位置。 然後，我們會將整個子樹移到新位置。  
  
`GetReparentedValue` 方法會使用兩個引數。 第一個引數描述要修改的階層部分。 例如，如果階層為 **/1/4/2/3/** 而您想要變更 **/1/4/** 區段，讓該階層變成 **/2/1/2/3/**，留下最後兩個節點 (**2/3/**) 不變，您必須提供變更的節點 (**/1/4/**) 作為第一個引數。 第二個引數會提供新的階層層級，在範例中為 **/2/1/**。 兩個引數不必包含相同的層級數目。  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>將單一資料列移到階層中的新位置  
  
1.  目前 Wanida 回報給 Sariya。 在此程序中，您會從目前的節點 **/1/1/,** 移動 Wanida，因此她會回報給 Jill。 她的新節點將會變成 **/3/1/** ，因此 **/1/** 是第一個引數，而 **/3/** 是第二個引數。 這些引數會對應到 Sariya 和 Jill 的 **OrgNode** 值。 執行下列程式碼，將 Wanida 從 Sariya 的組織移到 Jill 的組織：  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  執行下列程式碼以查看結果：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    Wanida 現在是在節點 **/3/1/**。  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>重新組織階層的區段  
  
1.  為示範如何同時移動大量的人員，請先執行下列程式碼，以便加一位實習生回報給 Wanida：  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  現在，Kevin 回報給 Wanida，Wanida 回報給 Jill，而 Jill 回報給 David。 也就是說，Kevin 位於層級 **/3/1/1/**。 若要將 Jill 的所有部屬移到新的主管之下，我們會將讓 **/3/** 當作其 **OrgNode** 的所有節點更新為新值。 執行下列程式碼，將 Wanida 更新為回報給 Sariya，但是讓 Kevin 回報給 Wanida：  
  
    ```sql  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  執行下列程式碼以查看結果：  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
曾經回報給 Jill (Wanida 和 Kevin) 的整個組織樹狀結構現在會回報給 Sariya。  
  
若要讓預存程序辨識階層的區段，請參閱 [移動子樹](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees)的＜移動子樹＞一節。  
  
