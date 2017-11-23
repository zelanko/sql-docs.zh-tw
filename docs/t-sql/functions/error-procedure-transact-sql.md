---
title: "ERROR_PROCEDURE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_PROCEDURE_TSQL
- ERROR_PROCEDURE
dev_langs: TSQL
helpviewer_keywords:
- ERROR_PROCEDURE function
- messages [SQL Server], trigger where occurred
- errors [SQL Server], stored procedure where occurred
- TRY...CATCH [SQL Server]
- CATCH block
- messages [SQL Server], stored procedure where occurred
- errors [SQL Server], trigger where occurred
ms.assetid: b81edbf0-856a-498f-ba87-48ff1426d980
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e13d4201a9381ca80a700fdb04fc69cf1044b664
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="errorprocedure-transact-sql"></a>ERROR_PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回發生錯誤造成執行 TRY…CATCH 建構的 CATCH 區塊之預存程序或觸發程序的名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ERROR_PROCEDURE ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （128)**  
  
## <a name="return-value"></a>傳回值  
 在 CATCH 區塊中呼叫時，會傳回發生錯誤的預存程序名稱。  
  
 如果未在預存程序或觸發程序內發生錯誤，便傳回 NULL。  
  
 如果是在 CATCH 區塊範圍之外呼叫，便傳回 NULL。  
  
## <a name="remarks"></a>備註  
 您可以在 CATCH 區塊範圍內的任何位置呼叫 ERROR_PROCEDURE。  
  
 ERROR_PROCEDURE 會傳回發生錯誤的預存程序或觸發程序的名稱，不論呼叫它的次數為何，或是在 CATCH 區塊範圍內的什麼位置呼叫它，都是如此。 這種函式，例如@ERROR，緊接著一個造成錯誤的陳述式中或在 CATCH 區塊的第一個陳述式中傳回的錯誤號碼。  
  
 在巢狀 CATCH 區塊中，ERROR_PROCEDURE 會傳回參考它的 CATCH 區塊範圍專用的預存程序或觸發程序的名稱。 例如，TRY…CATCH 建構的 CATCH 區塊可能會有巢狀的 TRY…CATCH。 在巢狀 CATCH 區塊內，ERROR_PROCEDURE 會傳回發生叫用巢狀 CATCH 區塊之錯誤的預存程序或觸發程序名稱。 如果 ERROR_PROCEDURE 是在外部 CATCH 區塊中執行，它會傳回發生叫用該 CATCH 區塊的錯誤之預存程序或觸發程序的名稱。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-errorprocedure-in-a-catch-block"></a>A. 在 CATCH 區塊中使用 ERROR_PROCEDURE  
 下列程式碼範例會顯示產生除以零的錯誤之預存程序。 `ERROR_PROCEDURE` 會傳回錯誤發生所在之預存程序的名稱。  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>B. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_PROCEDURE  
 下列程式碼範例會顯示產生除以零的錯誤之預存程序。 它會傳回發生錯誤的預存程序的名稱，以及錯誤的相關資訊。  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage,  
        ERROR_LINE() AS ErrorLine;  
        END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorprocedure-in-a-catch-block"></a>C. 在 CATCH 區塊中使用 ERROR_PROCEDURE  
 下列程式碼範例會顯示產生除以零的錯誤之預存程序。 `ERROR_PROCEDURE` 會傳回錯誤發生所在之預存程序的名稱。  
  
```  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_PROCEDURE() AS ErrorProcedure;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorprocedure-in-a-catch-block-with-other-error-handling-tools"></a>D. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_PROCEDURE  
 下列程式碼範例會顯示產生除以零的錯誤之預存程序。 它會傳回發生錯誤的預存程序的名稱，以及錯誤的相關資訊。  
  
```  
  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that   
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT   
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
        END CATCH;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

