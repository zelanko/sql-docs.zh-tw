---
title: 檢查 Employee 資料表的目前結構 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 620defd42e27b122a92ee145da6b4b14d1cbf996
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006635"
---
# <a name="lesson-1-1---examining-the-current-structure-of-the-employee-table"></a>第 1-1 課：檢查 Employee 資料表的目前結構
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] (或更新版本) 範例資料庫在 **HumanResources** 結構描述中包含一個 **Employee** 資料表。 為避免變更原始資料表，此步驟會製作一個名為 **EmployeeDemo** 的 **Employee**資料表複本。 若要簡化範例，您僅能從原始資料表複製五個資料行。 然後，您可以查詢 **HumanResources.EmployeeDemo** 資料表，以便在不使用 **hierarchyid** 資料類型的情況下，檢閱如何將資料表中的資料結構化。  
  
### <a name="to-copy-the-employee-table"></a>複製 Employee 資料表  
  
1.  在 [查詢編輯器] 視窗中執行下列程式碼，以便將資料表結構和資料從 **Employee** 資料表複製到名稱為 **EmployeeDemo**的新資料表。 由於原始的資料表已經使用 hierarchyid，此查詢基本上會使階層扁平化，以擷取員工的經理。 在本課程的後續部分中，我們將會重建此階層。
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
      (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
            WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
                (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID
        , emp.JobTitle, emp.HireDate
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee emp ;
    GO
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>檢查 EmployeeDemo 資料表的結構和資料  
  
-   這個新的 **EmployeeDemo** 資料表代表現有的資料庫中，您想要移轉成新結構的一般資料表。 在 [查詢編輯器] 視窗中，執行下列程式碼以顯示資料表如何使用自我聯結來顯示員工/主管關聯性：  
  
    ```  
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
    NULL    NULL    1   adventure-works\ken0    Chief Executive Officer
    1   adventure-works\ken0    2   adventure-works\terri0  Vice President of Engineering
    1   adventure-works\ken0    16  adventure-works\david0  Marketing Manager
    1   adventure-works\ken0    25  adventure-works\james1  Vice President of Production
    1   adventure-works\ken0    234 adventure-works\laura1  Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0   Information Services Manager
    1   adventure-works\ken0    273 adventure-works\brian3  Vice President of Sales
    2   adventure-works\terri0  3   adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0    Senior Tool Designer
    ...  
    ```  
  
    會繼續顯示結果，總共包含 290 個資料列。  
  
請注意， **ORDER BY** 子句會使輸出將每個管理階層的直屬員工列在一起。 例如，**MgrID** 1 (ken0) 的全部七個直屬員工會緊接著彼此列出。 雖然並非不可能，但是要將最終回報給 **MgrID** 1 的所有人員群組在一起更為困難。  
  
在下一項工作中，我們將建立資料類型為 **hierarchyid** 的新資料表，然後將資料移到這個新資料表中。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[使用現有的階層式資料填入資料表](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
  
