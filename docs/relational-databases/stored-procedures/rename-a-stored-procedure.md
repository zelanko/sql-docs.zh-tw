---
title: 重新命名預存程序 | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 2019 (15.x) 中重新命名預存程序。
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ddf1685f89d24c5b1b6dec4956c3e0c7542ac236
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332527"
---
# <a name="rename-a-stored-procedure"></a>重新命名預存程序

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重新命名 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要重新命名預存程序，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   程序名稱必須符合 [識別碼](../../relational-databases/databases/database-identifiers.md)的規則。  
  
-   重新命名預存程序會保留 `object_id` 及特別指派給此程序的所有權限。 卸除並重新建立物件會建立新的 `object_id`，並移除特別指派給此程序的任何權限。

-   重新命名預存程序不會變更 **sys.sql_modules** 目錄檢視 definition 資料行中對應的物件名稱。 若要那麼做，您必須卸除並重新建立具有新名稱的預存程序。  

-   變更程序的名稱或定義後，若未更新物件來反映對程序所做的變更，則可能導致相依物件執行失敗。 如需詳細資訊，請參閱 [檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 CREATE PROCEDURE  
 需要資料庫的 CREATE PROCEDURE 權限，以及要在其中建立程序之結構描述的 ALTER 權限，或者需要 **db_ddladmin** 固定資料庫角色的成員資格。  
  
 ALTER PROCEDURE  
 需要程序的 ALTER 權限，或 **db_ddladmin** 固定資料庫角色的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>若要重新命名預存程序  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
2.  依序展開 **[資料庫]** 、程序所屬的資料庫，以及 **[可程式性]** 。  
3.  [判斷預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)。  
4.  展開 [預存程序]，以滑鼠右鍵按一下要重新命名的程序，然後按一下 [重新命名]。  
5.  修改程序名稱。  
6.  修改在任何相依物件或指令碼中參考的程序名稱。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>若要重新命名預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
2.  在標準列中，按一下 **[新增查詢]** 。  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例示範如何藉由卸除程序，再以新名稱重新建立程序的方式重新命名程序。 第一個範例會建立 `'HumanResources.uspGetAllEmployeesTest`預存程序。 第二個範例會將預存程序重新命名為 `HumanResources.uspEveryEmployeeTest`。  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [修改預存程序](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [刪除預存程序](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [檢視預存程序的定義](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
