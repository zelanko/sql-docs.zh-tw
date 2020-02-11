---
title: 使用階層式方法重新排列階層式資料表中的資料順序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 7b8064c7-62c6-488d-84d2-57a5828fb907
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5f289257d64a691a93d44d63d2a30991227802e1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110105"
---
# <a name="reordering-data-in-a-hierarchical-table-using-hierarchical-methods"></a>使用階層式方法重新排列階層式資料表中的資料順序
  重新組織階層是常見的維護工作。 在這項工作中，我們將會使用 UPDATE 陳述式搭配 [GetReparentedValue](/sql/t-sql/data-types/getreparentedvalue-database-engine) 方法，先將單一資料列移到階層中的新位置。 然後，我們會將整個子樹移到新位置。  
  
 
  `GetReparentedValue` 方法會使用兩個引數。 第一個引數描述要修改的階層部分。 例如，如果階層為 **/1/4/2/3/** 而您想要變更 **/1/4/** 區段，讓該階層變成 **/2/1/2/3/**，留下最後兩個節點 (**2/3/**) 不變，您必須提供變更的節點 (**/1/4/**) 作為第一個引數。 第二個引數會提供新的階層層級，在範例中為 **/2/1/**。 兩個引數不必包含相同的層級數目。  
  
### <a name="to-move-a-single-row-to-a-new-location-in-the-hierarchy"></a>將單一資料列移到階層中的新位置  
  
1.  目前 Wanida 回報給 Sariya。 在此程序中，您會從目前的節點 **/1/1/,** 移動 Wanida，因此她會回報給 Jill。 她的新節點將會變成 **/3/1/** ，因此 **/1/** 是第一個引數，而 **/3/** 是第二個引數。 這些引數會對應到 Sariya 和 Jill 的 **OrgNode** 值。 執行下列程式碼，將 Wanida 從 Sariya 的組織移到 Jill 的組織：  
  
    ```  
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
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
     Wanida 現在是在節點 **/3/1/**。  
  
### <a name="to-reorganize-a-section-of-a-hierarchy"></a>重新組織階層的區段  
  
1.  為示範如何同時移動大量的人員，請先執行下列程式碼，以便加一位實習生回報給 Wanida：  
  
    ```  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  現在，Kevin 回報給 Wanida，Wanida 回報給 Jill，而 Jill 回報給 David。 也就是說，Kevin 位於層級 **/3/1/1/**。 若要將 Jill 的所有部屬移到新的主管之下，我們會將讓 **/3/** 當作其 **OrgNode** 的所有節點更新為新值。 執行下列程式碼，將 Wanida 更新為回報給 Sariya，但是讓 Kevin 回報給 Wanida：  
  
    ```  
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
/1/1//2      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
 曾經回報給 Jill (Wanida 和 Kevin) 的整個組織樹狀結構現在會回報給 Sariya。  
  
 若要讓預存程序辨識階層的區段，請參閱 [移動子樹](../hierarchical-data-sql-server.md#BKMK_MovingSubtrees)的＜移動子樹＞一節。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [摘要：在階層式資料表中管理資料](lesson-2-5-summary-managing-data-in-a-hierarchical-table.md)  
  
  
