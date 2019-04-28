---
title: 重新命名預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b85a6a5e79c004eb3ed2c7c40c6e3b62d526e95a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721009"
---
# <a name="rename-a-stored-procedure"></a>重新命名預存程序
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 重新命名 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要重新命名預存程序，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   程序名稱必須符合 [識別碼](../databases/database-identifiers.md)的規則。  
  
-   重新命名預存程序不會變更 **sys.sql_modules** 目錄檢視 definition 資料行中對應的物件名稱。 因此，我們建議您不要重新命名這個物件類型。 相反地，請卸除預存程序，再利用它的新名稱來重新建立預存程序。  
  
-   變更程序的名稱或定義後，若未更新物件來反映對程序所做的變更，則可能導致相依物件執行失敗。 如需詳細資訊，請參閱 [檢視預存程序的相依性](view-the-dependencies-of-a-stored-procedure.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 CREATE PROCEDURE  
 需要資料庫的 CREATE PROCEDURE 權限，以及將在其中建立程序之結構描述的 ALTER 權限，或者需要 **db_ddladmin** 固定資料庫角色的成員資格。  
  
 ALTER PROCEDURE  
 需要程序的 ALTER 權限，或 **db_ddladmin** 固定資料庫角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>若要重新命名預存程序  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]**、程序所屬的資料庫，以及 **[可程式性]**。  
  
3.  [判斷預存程序的相依性](view-the-dependencies-of-a-stored-procedure.md)。  
  
4.  展開 [預存程序]，以滑鼠右鍵按一下要重新命名的程序，然後按一下 [重新命名]。  
  
5.  修改程序名稱。  
  
6.  修改在任何相依物件或指令碼中參考的程序名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>若要重新命名預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何藉由卸除程序，再以新名稱重新建立程序的方式重新命名程序。 第一個範例會建立 `'HumanResources.uspGetAllEmployeesTest`預存程序。 第二個範例會將預存程序重新命名為 `HumanResources.uspEveryEmployeeTest`。  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspEveryEmployeeTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [建立預存程序](../stored-procedures/create-a-stored-procedure.md)   
 [修改預存程序](../stored-procedures/modify-a-stored-procedure.md)   
 [刪除預存程序](../stored-procedures/delete-a-stored-procedure.md)   
 [檢視預存程序的定義](view-the-definition-of-a-stored-procedure.md)   
 [檢視預存程序的相依性](view-the-dependencies-of-a-stored-procedure.md)  
  
  
