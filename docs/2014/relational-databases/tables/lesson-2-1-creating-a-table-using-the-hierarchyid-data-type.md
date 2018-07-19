---
title: 使用 hierarchyid 資料類型建立資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 0d1f361f-336c-4571-99d1-f4813b2d9fc4
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 92e0980e129aa43dcdd0d12c5b4001323504ee0b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323790"
---
# <a name="creating-a-table-using-the-hierarchyid-data-type"></a>使用 hierarchyid 資料類型建立資料表
  以下範例會建立名稱為 EmployeeOrg 的資料表，其中同時包含員工資料及其回報的階層。 這個範例會在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中建立資料表，但是這是選擇性的。 為了要維持此範例的簡單性，此資料表僅包含五個資料行：  
  
-   OrgNode 是一個 `hierarchyid` 資料行，其中儲存階層式關聯性。  
  
-   OrgLevel 是一個以 OrgNode 資料行為基礎的計算資料行，後者可將每個節點層級儲存在階層中。 它將會用於廣度優先的索引。  
  
-   EmployeeID 包含用於應用程式 (例如，薪資) 的一般員工識別碼。 在開發新應用程式時，這些應用程式可以使用 OrgNode 資料行，因此不需要另外的這個 EmployeeID 資料行。  
  
-   EmpName 包含員工的名稱。  
  
-   Title 包含員工的職稱。  
  
### <a name="to-create-the-employeeorg-table"></a>若要建立 EmployeeOrg 資料表  
  
1.  在 [查詢編輯器] 視窗中，執行下列程式碼來建立 `EmployeeOrg` 資料表。 指定 `OrgNode` 資料行做為具有叢集索引的主要索引鍵將會建立深度優先的索引：  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
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
  
    ```  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
 資料表現在已經準備好可以填寫資料。 下一個工作將是使用階層式方法擴展資料表。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [使用階層式方法擴展階層式資料表](lesson-2-2-populating-a-hierarchical-table-using-hierarchical-methods.md)  
  
  
