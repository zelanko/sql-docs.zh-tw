---
title: "ERROR_LINE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 11c3131f09669f87ec48a0ad3b1179c2b6df3327
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="errorline-transact-sql"></a>ERROR_LINE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回發生錯誤造成執行 TRY…CATCH 建構之 CATCH 區塊的行號。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ERROR_LINE ( )  
```  
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
 當在 CATCH 區塊內呼叫：  
  
-   傳回發生錯誤的行號。  
  
-   如果在預存程序或觸發程序內發生錯誤，就會傳回常式內的行號。  
  
 如果是在 CATCH 區塊範圍之外呼叫，便傳回 NULL。  
  
## <a name="remarks"></a>備註  
 可以在 CATCH 區塊範圍內的任何位置呼叫這個函數。  
  
 ERROR_LINE 會傳回呼叫它，或呼叫 CATCH 區塊範圍內的次數不論錯誤發生的行號。 這種函式，例如@ERROR，緊接著一個錯誤的陳述式中或在 CATCH 區塊的第一個陳述式中傳回的錯誤號碼。  
  
 在巢狀 CATCH 區塊中，ERROR_LINE 會傳回參考它的 CATCH 區塊範圍特定的錯誤行號。 例如，TRY…CATCH 建構的 CATCH 區塊可能包含巢狀的 TRY…CATCH 建構。 在巢狀 CATCH 區塊內，ERROR_LINE 會傳回呼叫巢狀 CATCH 區塊之錯誤的行號。 如果 ERROR_LINE 是在外部 CATCH 區塊內執行，它會傳回叫用這個 CATCH 區塊之錯誤的行號。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-errorline-in-a-catch-block"></a>A. 在 CATCH 區塊中使用 ERROR_LINE  
 下列程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 傳回發生錯誤的行號。  
  
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
  
### <a name="b-using-errorline-in-a-catch-block-with-a-stored-procedure"></a>B. 在含有預存程序的 CATCH 區塊中使用 ERROR_LINE  
 下列程式碼範例顯示將會產生除以零之錯誤的預存程序。 `ERROR_LINE` 會傳回預存程序中發生錯誤的行號。  
  
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
  
### <a name="c-using-errorline-in-a-catch-block-with-other-error-handling-tools"></a>C. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_LINE  
 下列程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 它會傳回發生錯誤的行號以及錯誤的相關資訊。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
