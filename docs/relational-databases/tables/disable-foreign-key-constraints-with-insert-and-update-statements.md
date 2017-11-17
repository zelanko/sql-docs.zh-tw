---
title: "停用 INSERT 和 UPDATE 陳述式的外部索引鍵條件約束 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
- UPDATE statement [SQL Server], foreign key constraints
- INSERT statement [SQL Server], foreign key constraints
ms.assetid: 029168d7-085e-4b13-9b86-5644b67c6e24
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a72cfad873d2fe891c9f10c3c5f8c0ede3a68ff2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="disable-foreign-key-constraints-with-insert-and-update-statements"></a>停用 INSERT 和 UPDATE 陳述式的外部索引鍵條件約束
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中停用 INSERT 和 UPDATE 交易期間的外部索引鍵條件約束。 如果您確知新資料將違反現有條件約束，或是條件約束只適用於已經在資料庫中的資料，請使用此選項。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法停用 INSERT 和 UPDATE 陳述式的外部索引鍵條件約束：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 停用這些條件約束之後，未來將不會根據條件約束的條件驗證資料行的插入或更新作業。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要資料表的 ALTER 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>若要停用 INSERT 和 UPDATE 陳述式的外部索引鍵條件約束  
  
1.  在 **[物件總管]**中，展開含有條件約束的資料表，然後展開 **[索引鍵]** 資料夾。  
  
2.  以滑鼠右鍵按一下條件約束，然後選取 **[修改]**。  
  
3.  在 **[資料表設計工具]**底下的方格中，按一下 **[強制使用外部索引鍵條件約束]** ，然後從下拉式功能表中選取 **[否]** 。  
  
4.  按一下 [ **關閉**]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>若要停用 INSERT 和 UPDATE 陳述式的外部索引鍵條件約束  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT FK_PurchaseOrderHeader_Employee_EmployeeID;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
###  <a name="TsqlExample"></a>  

