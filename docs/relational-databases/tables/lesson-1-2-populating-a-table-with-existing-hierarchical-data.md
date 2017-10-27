---
title: "使用現有的階層式資料填入資料表 | Microsoft Docs"
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
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4569fb3f5bc56d04624756eb3fccba8da1d4ad2f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-2---populating-a-table-with-existing-hierarchical-data"></a>第 1-2 課：使用現有的階層式資料填入資料表
此工作會建立一個新的資料表，並以 **EmployeeDemo** 資料表中的資料填入該資料表。 此工作的步驟如下：  
  
-   建立包含 **hierarchyid** 資料行的新資料表。 此資料行可以取代現有的 **EmployeeID** 和 **ManagerID** 資料行。 不過，您將會保留這些資料行。 這是因為現有的應用程式可能會參考這些資料行，而且這些資料行也可以在轉換後，協助您了解資料。 資料表定義指定 **OrgNode** 為主索引鍵，其會要求該資料行所包含的值不得重複。 **OrgNode** 資料行上的叢集索引將以 **OrgNode** 順序儲存資料。  
  
-   建立暫存資料表，該資料表可用於追蹤各個主管手下的直屬員工人數。  
  
-   使用 **EmployeeDemo** 資料表中的資料，填入新資料表。  
  
### <a name="to-create-a-new-table-named-neworg"></a>若要建立名稱為 NewOrg 的新資料表  
  
-   在 [查詢編輯器] 視窗中，執行下列程式碼以建立名稱為 **HumanResources.NewOrg**的新資料表：  
  
    ```  
    CREATE TABLE NewOrg  
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
  
### <a name="to-create-a-temporary-table-named-children"></a>建立名稱為 #Children 的暫存資料表  
  
1.  建立名為 **#Children** 的暫存資料表，以及名稱為 **Num** 的資料行，該資料行將包含每個節點的子系數目：  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  新增索引以大幅提高填入 **NewOrg** 資料表的查詢速度：  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>填入 NewOrg 資料表  
  
1.  遞迴查詢禁止包含彙總的子查詢。 反之，會使用下列程式碼填入 **#Children** 資料表；該程式碼是使用 [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) 方法填入 **Num** 資料行：  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  檢閱 **#Children** 資料表。 請注意 **Num** 資料行如何包含每個主管的序號。  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    `EmployeeID ManagerID Num`  
  
    `---------- --------- ---`  
  
    `1        NULL       1`  
  
    `2         1         1`  
  
    `3         1         2`  
  
    `4         2         1`  
  
    `5         2         2`  
  
    `6         2         3`  
  
    `7         3         1`  
  
    `8         3         2`  
  
    `9         4         1`  
  
    `10        4         2`  
  
3.  填入 **NewOrg** 資料表。 使用 GetRoot 和 ToString 方法，將 **Num** 值串連到 **hierarchyid** 格式，然後以產生的階層式值更新 **OrgNode** 資料行：  
  
    ```  
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
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  將 **hierarchyid** 資料行轉換為字元格式時，會比較容易了解該資料行。 執行下列程式碼 (其中包含 **OrgNode** 資料行之兩種表示法)，以檢閱 **NewOrg** 資料表中的資料：  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
    **LogicalNode** 資料行會將 **hierarchyid** 資料行轉換為更容易讀取之代表階層的文字格式。 在其餘工作中，您將使用 `ToString()` 方法，顯示 **hierarchyid** 資料行的邏輯格式。  
  
5.  卸除不再需要的暫存資料表：  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
下一個工作將是建立索引以支援階層式結構。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[最佳化 NewOrg 資料表](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
  
  

