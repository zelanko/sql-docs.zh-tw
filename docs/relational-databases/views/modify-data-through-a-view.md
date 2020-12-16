---
description: 透過檢視修改資料
title: 透過檢視修改資料 | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d606d4a6cad0668f3692af38a1ec7d2f2a1f1db6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484400"
---
# <a name="modify-data-through-a-view"></a>透過檢視修改資料
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  您可使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 SQL Server 中修改基礎基底資料表的資料。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md) 中的＜可更新的檢視＞一節。  
  
  
###  <a name="permissions"></a><a name="Permissions"></a> 權限  
 根據執行的動作，需要目標資料表的 UPDATE、INSERT 或 DELETE 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>透過檢視修改資料表資料  
  
1.  在 **[物件總管]** 中，展開包含檢視的資料庫，然後展開 **[檢視]** 。  
  
2.  以滑鼠右鍵按一下檢視，然後選取 [編輯前 200 個資料列]  。  
  
3.  您可能需要修改 **[SQL]** 窗格中的 SELECT 陳述式，才能傳回要修改的資料列。  
  
4.  在 **[結果]** 窗格中，尋找要變更或刪除的資料列。 若要刪除資料列，請以滑鼠右鍵按一下此資料列，然後選取 [刪除]  。 若要變更一個或多個資料行中的資料，請修改資料行中的資料。  
  
    > **重要！！** 如果檢視參考多個基底資料表，就不能刪除資料列。 您只可以更新屬於單一基底資料表的資料行。  
  
5.  若要插入資料列，向下捲動到資料列的結尾，然後插入新值。  

    > **重要！** 如果檢視參考多個基底資料表，就不能插入資料列。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>透過檢視更新資料表資料  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會透過參考 `StartDate` 檢視中的資料行，變更特定員工的 `EndDate` 和 `HumanResources.vEmployeeDepartmentHistory`資料行值。 此檢視從兩個資料表傳回值。 此陳述式會成功，因為修改的資料行只來自其中一個基底資料表。  
  
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
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例會藉由指定 `HumanResouces.Department` 檢視中的相關資料行，將新資料列插入 `HumanResources.vEmployeeDepartmentHistory`基底資料表。 此陳述式會成功，因為只指定單一基底資料表中的資料行，而且此基底資料表中的其他資料行有預設值。  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 如需詳細資訊，請參閱 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)。  
  
  
