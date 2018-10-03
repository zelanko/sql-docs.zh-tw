---
title: 最佳化 NewOrg 資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a031466e35fef90104ab81fec17010725f8f5c0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146978"
---
# <a name="optimizing-the-neworg-table"></a>最佳化 NewOrg 資料表
  **NewOrd**中所建立的資料表[使用現有的階層式資料填入資料表](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)工作包含所有員工資訊，並使用代表階層結構`hierarchyid`資料類型。 此工作會加入新索引以支援在 `hierarchyid` 資料行上進行搜尋。  
  
## <a name="clustered-index"></a>叢集索引  
 `hierarchyid`資料行 (**OrgNode**) 是主索引鍵**NewOrg**資料表。 建立資料表時，它包含名為 **PK_NewOrg_OrgNode** 的叢集索引以強制 **OrgNode** 資料行的唯一性。 此叢集索引也支援深度優先的資料表搜尋。  
  
## <a name="nonclustered-index"></a>非叢集索引  
 此步驟會建立兩個非叢集索引來支援一般搜尋。  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>建立 NewOrg 資料表的索引以便進行有效率的搜尋  
  
1.  為協助在階層的相同層級進行查詢，使用 [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) 方法來建立階層中包含層級的計算資料行。 然後，在層級和 `Hierarchyid` 上建立複合式索引。 執行下列程式碼以建立計算資料行和廣度優先的索引：  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  在 **EmployeeID** 資料行上建立唯一的索引。 這是依 **EmployeeID** 號碼之單一員工的傳統單一查閱。 執行下列程式碼，在 **EmployeeID**上建立索引：  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  執行下列程式碼，以全部三個索引的順序，從資料表擷取資料：  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  比較結果集以查看每個索引類型中儲存的順序。 只有每個輸出的前四個資料列遵照這個順序。  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     深度優先索引：員工記錄緊接著其主管儲存。  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     **EmployeeID** 優先索引：資料列會以 **EmployeeID** 順序儲存。  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
>  如需顯示深度優先索引與廣度優先索引間差異的圖表，請參閱[階層式資料 &#40;SQL Server&#41;](../hierarchical-data-sql-server.md)。  
  
#### <a name="to-drop-the-unnecessary-columns"></a>卸除不必要的資料行  
  
1.  **ManagerID** 資料行代表員工/主管的關聯性，此種關聯性現在以 **OrgNode** 資料行代表。 如果其他應用程式不需要 **ManagerID** 資料行，請考慮使用下列陳述式卸除該資料行：  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  **EmployeeID** 資料行也是多餘的。 **OrgNode** 資料行可唯一識別每個員工。 如果其他應用程式不需要 **EmployeeID** 資料行，請考慮使用下列程式碼先卸除索引，再卸除該資料行：  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>以新的資料表取代原始的資料表  
  
1.  如果您的原始資料表包含任何額外的索引或條件約束，請將它們新增到 **NewOrg** 資料表中。  
  
2.  以新的資料表取代舊的 **EmployeeDemo** 資料表。 執行下列程式碼卸除舊的資料表，然後以舊名稱重新命名新的資料表：  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  執行下列程式碼檢查最終的資料表：  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [摘要：將資料表轉換為階層式結構](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
