---
title: "透過檢視修改資料 | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a7ffd77db6d7d3d68e52ce423b206d84d002d0c5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="modify-data-through-a-view"></a>透過檢視修改資料
  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中修改基礎基底資料表的資料。  
  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md) 中的＜可更新的檢視＞一節。  
  
  
###  <a name="Permissions"></a> Permissions  
 根據執行的動作，需要目標資料表的 UPDATE、INSERT 或 DELETE 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>透過檢視修改資料表資料  
  
1.  在 **[物件總管]**中，展開包含檢視的資料庫，然後展開 **[檢視]**。  
  
2.  以滑鼠右鍵按一下檢視，然後選取 [編輯前 200 個資料列]。  
  
3.  您可能需要修改 **[SQL]** 窗格中的 SELECT 陳述式，才能傳回要修改的資料列。  
  
4.  在 **[結果]** 窗格中，尋找要變更或刪除的資料列。 若要刪除資料列，請以滑鼠右鍵按一下此資料列，然後選取 [刪除]。 若要變更一個或多個資料行中的資料，請修改資料行中的資料。  
  
    > **重要！！** 如果檢視參考多個基底資料表，就不能刪除資料列。 您只可以更新屬於單一基底資料表的資料行。  
  
5.  若要插入資料列，向下捲動到資料列的結尾，然後插入新值。  
  
    > **重要！** 如果檢視參考多個基底資料表，就不能插入資料列。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>透過檢視更新資料表資料  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會透過參考 `StartDate` 檢視中的資料行，變更特定員工的 `EndDate` 和 `HumanResources.vEmployeeDepartmentHistory`資料行值。 此檢視從兩個資料表傳回值。 此陳述式會成功，因為修改的資料行只來自其中一個基底資料表。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)。  
  
#### <a name="to-insert-table-data-through-a-view"></a>透過檢視插入資料表資料  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例會藉由指定 `HumanResouces.Department` 檢視中的相關資料行，將新資料列插入 `HumanResources.vEmployeeDepartmentHistory`基底資料表。 此陳述式會成功，因為只指定單一基底資料表中的資料行，而且此基底資料表中的其他資料行有預設值。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)。  
  
  
