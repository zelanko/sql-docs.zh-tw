---
title: ERROR_LINE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3e6562b656695963868e849a063796ea70c3d097
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948835"
---
# <a name="errorline-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函式會傳回發生錯誤造成執行 TRY...CATCH 建構之 CATCH 區塊的行號。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>傳回類型  
**int**  
  
## <a name="return-value"></a>傳回值  
在 CATCH 區塊中呼叫時，`ERROR_LINE` 會傳回  
  
-   發生錯誤的行號    
-   常式中的行號 (如果在預存程序或觸發程序內發生錯誤)  
-   NULL (如果在 CATCH 區塊範圍之外呼叫)。  
  
## <a name="remarks"></a>Remarks  
可以在 CATCH 區塊範圍內的任何位置呼叫 `ERROR_LINE`。  
  
`ERROR_LINE` 會傳回發生錯誤的行號。 不論在 CATCH 區塊範圍內的哪個位置呼叫 `ERROR_LINE`，以及呼叫 `ERROR_LINE` 的次數為何，都是如此。 這有別於 @ERROR 之類的函式。 @ERROR 會在緊接於發生錯誤的陳述式之後的陳述式中，或在 CATCH 區塊的第一個陳述式中，傳回錯誤號碼。  
  
在巢狀 CATCH 區塊中，`ERROR_LINE` 會傳回參考它的 CATCH 區塊範圍特定的錯誤行號。 例如，TRY...CATCH 建構的 CATCH 區塊可能包含巢狀的 TRY...CATCH 建構。 在巢狀 CATCH 區塊內，`ERROR_LINE` 會傳回叫用巢狀 CATCH 區塊之錯誤的行號。 如果 `ERROR_LINE` 是在外部 CATCH 區塊內執行，它會傳回叫用該特定 CATCH 區塊之錯誤的行號。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-errorline-in-a-catch-block"></a>A. 在 CATCH 區塊中使用 ERROR_LINE  
此程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 `ERROR_LINE` 會傳回發生錯誤的行號。  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
Result 
-----------

(0 row(s) affected)

ErrorLine
-----------
4

(1 row(s) affected)
```  
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>B. 在含有預存程序的 CATCH 區塊中使用 ERROR_LINE  
此範例會顯示產生除以零之錯誤的預存程序。 `ERROR_LINE` 會傳回發生錯誤的行號。  
  
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
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorLine
-----------
7

(1 row(s) affected)  
   
```

### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>C. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_LINE  
此程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 `ERROR_LINE` 會傳回發生錯誤的行號，以及與錯誤本身相關的資訊。  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
``` 
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
```  
-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState ErrorProcedure ErrorLine ErrorMessage
----------- ------------- ---------- -------------- --------- ---------------------------------
8134        16            1          NULL           3         Divide by zero error encountered.

(1 row(s) affected)
  
```
  
## <a name="see-also"></a>另請參閱  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
