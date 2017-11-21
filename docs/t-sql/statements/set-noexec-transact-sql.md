---
title: "SET NOEXEC (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NOEXEC_TSQL
- SET_NOEXEC_TSQL
- SET NOEXEC
- NOEXEC
dev_langs:
- TSQL
helpviewer_keywords:
- queries [SQL Server], compiling
- SET NOEXEC statement
- compiling queries [SQL Server]
- NOEXEC option
ms.assetid: ba56fba1-af9b-4459-b6e4-5d7e71a7630b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09ea3fafe9537dea15aced1dac43e2ec07ceb674
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-noexec-transact-sql"></a>SET NOEXEC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  編譯每項查詢，但不執行它。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET NOEXEC { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 當 SET NOEXEC 是 ON 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會編譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的每個批次，但不會執行它們。 當 SET NOEXEC 是 OFF 時，就會在編譯之後執行所有批次。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行陳述式有兩個階段：編譯和執行。 在執行時，這項設定可用來使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼中的語法和物件名稱。 它也可用來偵錯通常是在較大的陳述式批次中的陳述式。  
  
 SET NOEXEC 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例搭配有效的查詢、含無效物件名稱的查詢，以及語法不正確的查詢來使用 `NOEXEC`。  
  
```  
USE AdventureWorks2012;  
GO  
PRINT 'Valid query';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Inner join.  
SELECT e.BusinessEntityID, e.JobTitle, v.Name  
FROM HumanResources.Employee AS e   
   INNER JOIN Purchasing.PurchaseOrderHeader AS poh  
   ON e.BusinessEntityID = poh.EmployeeID  
   INNER JOIN Purchasing.Vendor AS v  
   ON poh.VendorID = v.BusinessEntityID;  
GO  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid object name';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Function name uses is a reserved keyword.  
USE AdventureWorks2012;  
GO  
CREATE FUNCTION dbo.Values(@BusinessEntityID int)  
RETURNS TABLE  
AS  
RETURN (SELECT PurchaseOrderID, TotalDue  
   FROM dbo.PurchaseOrderHeader  
   WHERE VendorID = @BusinessEntityID);  
  
-- SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
  
PRINT 'Invalid syntax';  
GO  
-- SET NOEXEC to ON.  
SET NOEXEC ON;  
GO  
-- Built-in function incorrectly invoked.  
SELECT *  
FROM fn_helpcollations;  
-- Reset SET NOEXEC to OFF.  
SET NOEXEC OFF;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)  
  
  

