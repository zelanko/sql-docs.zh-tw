---
title: "ERROR_MESSAGE (TRANSACT-SQL) |Microsoft 文件"
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
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: ad4e69ea267af2a9575558737e17e79bbdad684f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回造成執行 TRY…CATCH 建構之 CATCH 區塊的錯誤訊息文字。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>傳回值  
 當它在 CATCH 區塊中被呼叫時，會傳回造成執行 CATCH 區塊之錯誤訊息的完整文字。 文字包括提供給任何可替代參數的值，例如，長度、物件名稱或次數。  
  
 如果是在 CATCH 區塊範圍之外呼叫，便傳回 NULL。  
  
## <a name="remarks"></a>備註  
 可以在 CATCH 區塊範圍內的任何位置呼叫 ERROR_MESSAGE。  
  
 不論執行多少次，也不論是在 CATCH 區塊範圍內的任何位置執行，ERROR_MESSAGE 都會傳回錯誤訊息。 這是相較於函式，例如 @@ERROR、 在陳述式之後，立即會造成錯誤，只傳回錯誤號碼或第一個陳述式的 CATCH 區塊。  
  
 在巢狀 CATCH 區塊中，ERROR_MESSAGE 會傳回參考它的 CATCH 區塊範圍特定的錯誤訊息。 例如，外部 TRY...CATCH 建構的 CATCH 區塊可能會有巢狀的 TRY...CATCH 建構。 在巢狀 CATCH 區塊內，ERROR_MESSAGE 會從叫用巢狀 CATCH 區塊的錯誤傳回訊息。 如果 ERROR_MESSAGE 是在外部 CATCH 區塊中執行，它會從叫用 CATCH 區塊的錯誤傳回訊息。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. 在 CATCH 區塊中使用 ERROR_MESSAGE  
 下列程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 它會傳回錯誤的訊息。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_MESSAGE  
 下列程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 錯誤的相關訊息會隨同錯誤訊息而一起傳回。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>C. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_MESSAGE  
 下列程式碼範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 錯誤的相關訊息會隨同錯誤訊息而一起傳回。  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  


