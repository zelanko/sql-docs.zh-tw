---
title: "使用階層式方法填入階層式資料表 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e4d9493f0abe60af4e4c063223cef63a080ed13f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-2---populating-a-hierarchical-table-using-hierarchical-methods"></a>第 2-2 課：使用階層式方法填入階層式資料表
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 行銷部門有 8 名員工。 員工層級如下：  
  
**David**( **EmployeeID** 6) 是行銷經理。 **David**管理三名行銷專員：  
  
-   **Sariya**( **EmployeeID** 46)  
  
-   **John**( **EmployeeID** 271)  
  
-   **Jill**( **EmployeeID** 119)  
  
**Sariya** 管理行銷助理**Wanida** ( **EmployeeID**269)， **John** 管理行銷助理**Mary** ( **EmployeeID**272)。  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>插入階層樹狀結構的根目錄  
  
1.  下列範例會將行銷經理 **David** 插入階層根目錄的資料表中。 **OrdLevel** 資料行為計算資料行。 因此，不是 INSERT 陳述式的一部分。 第一筆記錄使用 [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) 方法，將這個第一筆記錄擴展為階層的根目錄。  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  執行下列節點以檢查資料表中的初始資料列：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
如同上一個課程，我們使用 `ToString()` 方法，將 **hierarchyid** 資料類型轉換為比較容易了解的格式。  
  
### <a name="to-insert-a-subordinate-employee"></a>插入從屬員工  
  
1.  **David** 管理 **Sariya**。 若要插入 **Sariya** 的節點，您必須建立適合 **hierarchyid** 資料類型的 **OrgNode**值。 下列程式碼會建立 **hierarchyid** 資料類型的變數，並使用資料表的 OrgNode 根目錄值擴展。 然後，搭配 [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) 方法使用該變數來插入從屬節點的資料列。 `GetDescendant` 會採用兩個引數。 檢閱下列引數值的選項：  
  
    -   如果父系為 NULL， `GetDescendant` 會傳回 NULL。  
  
    -   如果父系不是 NULL，而 child1 和 child2 都是 NULL， `GetDescendant` 則會傳回父系的一個子系。  
  
    -   如果父系和 child1 都不是 NULL，而 child2 是 NULL， `GetDescendant` 會傳回父系中大於 child1 的子系。  
  
    -   如果父系和 child2 不是 NULL，而 child1 是 NULL， `GetDescendant` 會傳回父系中小於 child2 的子系。  
  
    -   如果父系、child1 和 child2 都不是 NULL， `GetDescendant` 會傳回父系中大於 child1 且小於 child2 的子系。  
  
    下列程式碼使用根目錄父系的 `(NULL, NULL)` 引數，因為除了根目錄之外，資料表中還沒有任何資料列。 執行下列程式碼以插入 **Sariya**：  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  從第一個程序開始重複查詢，以查詢資料表並查看項目如何出現：  
  
    ```  
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
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>建立輸入新節點的程序  
  
1.  若要簡化輸入資料的方式，請建立下列預存程序，將員工新增到 **EmployeeOrg** 資料表中。 該程序會接受要新增之員工的輸入值。 這包括新員工之主管的 **EmployeeID** 、新員工的 **EmployeeID** 號碼，及其姓氏和職稱。 此程序會使用 `GetDescendant()` 以及 [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) 方法。 執行下列程式碼以建立程序：  
  
    ```  
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
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  再次執行下列查詢，檢查 **EmployeeOrg** 資料表中的資料列：  
  
    ```  
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
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
資料表現在已經完全擴展到行銷組織了。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[使用階層方法查詢階層式資料表](../../relational-databases/tables/lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
  

