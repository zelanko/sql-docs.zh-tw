---
title: ERROR_NUMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_NUMBER_TSQL
- ERROR_NUMBER
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], numbers
- TRY...CATCH [SQL Server]
- ERROR_NUMBER function
- CATCH block
ms.assetid: 1de85fff-1ca2-4b31-841b-926e571cb150
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9ae22c38ef34ad8db35c625de80d47f08a0e6073
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250011"
---
# <a name="errornumber-transact-sql"></a>ERROR_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函式會傳回造成執行 TRY…CATCH 建構的 CATCH 區塊之錯誤的錯誤號碼。  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ERROR_NUMBER ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
在 CATCH 區塊中呼叫時，`ERROR_NUMBER` 會傳回造成執行 CATCH 區塊之錯誤的錯誤號碼。  

在 CATCH 區塊範圍之外呼叫時，`ERROR_NUMBER` 會傳回 NULL。  
  
## <a name="remarks"></a>Remarks  
`ERROR_NUMBER` 支援在 CATCH 區塊範圍內的任何位置呼叫。  
  
不論執行多少次，或在 `CATCH` 區塊範圍內的哪個位置執行，`ERROR_NUMBER` 都會傳回相關的錯誤號碼。 這有別於 @@ERROR 之類的函式，它們只會在緊接於發生錯誤的陳述式之後的陳述式中，傳回錯誤號碼。  

在巢狀 `CATCH` 區塊中，`ERROR_NUMBER` 會參考該 `CATCH` 區塊之 `CATCH` 區塊範圍特定的錯誤號碼。 例如，外部 TRY...CATCH 建構的 `CATCH` 區塊可能會有內部 `TRY...CATCH` 建構。 在該內部 `CATCH` 區塊內，`ERROR_NUMBER` 會傳回叫用內部 `CATCH` 區塊之錯誤的號碼。 如果 `ERROR_NUMBER` 是在外部 `CATCH` 區塊中執行，它會傳回叫用該外部 `CATCH` 區塊之錯誤的號碼。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-errornumber-in-a-catch-block"></a>A. 在 CATCH 區塊中使用 ERROR_NUMBER  
此範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 `CATCH` 區塊會傳回錯誤號碼。  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_NUMBER() AS ErrorNumber;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorNumber
-----------
8134

(1 row(s) affected)

```  
  
### <a name="b-using-errornumber-in-a-catch-block-with-other-error-handling-tools"></a>B. 在含有其他錯誤處理工具的 CATCH 區塊中使用 ERROR_NUMBER  
此範例會顯示產生除以零之錯誤的 `SELECT` 陳述式。 除了錯誤號碼，`CATCH` 區塊也會傳回該錯誤的相關資訊。  

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

-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure   ErrorLine  ErrorMessage
----------- ------------- ----------- ---------------  ---------- ----------------------------------
8134        16            1           NULL             4          Divide by zero error encountered.

(1 row(s) affected)

```  
  
## <a name="see-also"></a>另請參閱  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  

