---
title: "使用階層方法查詢階層式資料表 | Microsoft Docs"
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
helpviewer_keywords:
- HierarchyID
ms.assetid: 3b4f7dae-65b5-4d8d-8641-87aba9aa692d
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: af8bdce0dd68fbf33d364757cbb07d60054b1100
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-3---querying-a-hierarchical-table-using-hierarchy-methods"></a>第 2-3 課：使用階層方法查詢階層式資料表
既然 HumanResources.EmployeeOrg 資料表會完全擴展，此工作將會顯示如何使用某些階層式方法查詢階層。  
  
### <a name="to-find-subordinate-nodes"></a>尋找從屬節點  
  
1.  Sariya 有一個從屬員工。 若要查詢 Sariya 的部屬，請執行使用 [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) 方法的下列查詢：  
  
    ```  
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
  
    ```  
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
  
    ```  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    這次，您也可以接收到兩個層級下的 Mary，她也是回報給 David。  
  
### <a name="to-use-getroot-and-getlevel"></a>使用 GetRoot 與 GetLevel  
  
1.  階層成長得越大時，判斷成員在階層中的位置時，也就變得更加困難。 使用 [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) 方法，尋找階層中，每個資料列下有多少層級。 執行下列程式碼以檢視所有資料列的層級：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  使用 [GetRoot](../../t-sql/data-types/getroot-database-engine.md) 方法，尋找階層中的根節點。 下列程式碼範例會傳回根目錄的單一資料列：  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
  
下一個工作將會重新組織階層。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[使用階層式方法重新排列階層式資料表中的資料順序](../../relational-databases/tables/lesson-2-4-reordering-data-in-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
  

