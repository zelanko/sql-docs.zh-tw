---
title: 重新編譯預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sp_recompile
- WITH RECOMPILE clause
- recompiling stored procedures
- stored procedures [SQL Server], recompiling
ms.assetid: b90deb27-0099-4fe7-ba60-726af78f7c18
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d5b995bbe480eb67627a4cb796a6d5c58ddba07a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="recompile-a-stored-procedure"></a>重新編譯預存程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 重新編譯 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的預存程序。 執行這項操作的方法有三種：程序定義中或呼叫程序時的 **WITH RECOMPILE** 選項、個別陳述式上的 **RECOMPILE** 查詢提示，或是藉由使用 **sp_recompile** 系統預存程序。 本主題描述在建立程序定義及執行現有程序時使用 WITH RECOMPILE 選項。 另外還會描述使用 sp_recompile 系統預存程序重新編譯現有的程序。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用下列方法重新編譯預存程序：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   初次編譯或重新編譯程序時，該程序的查詢計劃會針對資料庫及其物件目前的狀態最佳化。 如果資料庫的資料或結構經歷大幅變更，則重新編譯程序時，會針對這些變更更新並最佳化程序的查詢計劃。 如此可以提高程序的處理效能。  
  
-   有時候程序必須強制重新編譯，有時候則會自動重新編譯。 只要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動，自動重新編譯就會發生。 若程序所參考的基礎資料表經過實體設計變更，則也會進行重新編譯。  
  
-   另一個強制程序重新編譯的理由是可以抵制程序編譯的「參數探測」行為。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行程序時，程序在編譯時所使用的任何參數值都會包含在產生查詢計畫的過程中。 如果這些值代表程序後續呼叫的典型值，則程序在每次編譯和執行時都可獲得查詢計劃的好處。 如果程序上的參數值經常是非典型的，則依據不同參數值強制重新編譯程序及新計畫可改善效能。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特色功能在於程序的陳述式層級重新編譯。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新編譯預存程序時，只會編譯造成重新編譯的陳述式，而不是完整程序。  
  
-   如果程序中的特定查詢固定使用非典型或暫存值，則可在這些查詢中使用 RECOMPILE 查詢提示來改善程序效能。 由於只會重新編譯使用查詢提示的查詢，而非完整程序，因此會模仿 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的陳述式層級重新編譯行為。 不過，除了使用程序目前的參數值之外，RECOMPILE 查詢提示也會在您編譯陳述式時，使用預存程序內任何區域變數的值。 如需詳細資訊，請參閱 [查詢提示 (Transact-SQL)](../../t-sql/queries/hints-transact-sql-query.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 **WITH RECOMPILE** 選項  
 如果在建立程序定義時使用此選項，則需要資料庫的 CREATE PROCEDURE 權限以及建立程序所在結構描述的 ALTER 權限。  
  
 如果在 EXECUTE 陳述式中使用此選項，則需要程序的 EXECUTE 權限。 EXECUTE 陳述式本身並不需要權限，但是 EXECUTE 陳述式中參考的程序需要執行權限。 如需詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)。  
  
 **RECOMPILE** 查詢提示  
 此功能是在建立程序時使用，而且提示會包含在程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中。 因此，它需要資料庫的 CREATE PROCEDURE 權限，以及建立程序所在結構描述的 ALTER 權限。  
  
 **sp_recompile** 系統預存程序  
 需要指定之程序的 ALTER 權限。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>若要使用 WITH RECOMPILE 選項重新編譯預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例會建立程序定義。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-the-with-recompile-option"></a>若要使用 WITH RECOMPILE 選項重新編譯預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例所建立的簡單程序會從檢視表傳回所有員工 (所提供的姓氏和名字)、工作職稱及部門名稱。  
  
     接著將第二個程式碼範例複製並貼到查詢視窗中，然後按一下 **[執行]**。 這樣就會執行程序，並重新編譯程序的查詢計劃。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXECUTE HumanResources.uspGetAllEmployees WITH RECOMPILE;  
GO  
  
```  
  
#### <a name="to-recompile-a-stored-procedure-by-using-sprecompile"></a>若要使用 sp_recompile 重新編譯預存程序  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例所建立的簡單程序會從檢視表傳回所有員工 (所提供的姓氏和名字)、工作職稱及部門名稱。  
  
     接著將下列範例複製並貼到查詢視窗中，並按一下 **[執行]**。 這樣並不會執行程序，但會標示要重新編譯的程序，以便在下一次執行程序時更新其查詢計畫。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'HumanResources.uspGetAllEmployees';  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [修改預存程序](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [重新命名預存程序](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [檢視預存程序的定義](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
