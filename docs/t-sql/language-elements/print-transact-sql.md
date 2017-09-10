---
title: "列印 (TRANSACT-SQL) |Microsoft 文件"
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
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51377ebe291fe4c76d8761aaba74eab8f5201108
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="print-transact-sql"></a>列印 Transact SQL
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  向用戶端傳回使用者自訂訊息。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  

PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>引數  
 *msg_str*  
 這是一個字元字串或 Unicode 字串常數。 如需詳細資訊，請參閱[常數 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@***local_variable*  
 這是任何有效字元資料類型的變數。 **@***local_variable*必須**char**， **nchar**， **varchar**，或**nvarchar**，或必須是能夠在隱含地轉換成這些資料類型。  
  
 *string_expr*  
 這是傳回字串的運算式。 它可以包括串連的常值、函數和變數。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
## <a name="remarks"></a>備註  
 如果訊息字串不是 Unicode 字串，它的長度可以多達 8,000 個字元；如果它是 Unicode 字串，則可以多達 4,000 個字元。 較長字串會被截斷。 **Varchar （max)**和**nvarchar （max)**資料型別會被截斷成資料類型都不能大於**varchar(8000)**和**nvarchar（4000)**.  
  
 RAISERROR 也可用來傳回訊息。 相較於 PRINT，RAISERROR 有下列優點：  
  
-   RAISERROR 支援利用以 C 語言標準程式庫 printf 函數為基礎來建立型模的機制，將引數代入錯誤訊息中。  
  
-   除了文字訊息之外，RAISERROR 還可以指定唯一錯誤號碼、嚴重性和狀態碼。  
  
-   RAISERROR 可用來傳回利用 sp_addmessage 系統預存程序建立的使用者自訂訊息。  
  
## <a name="examples"></a>範例  
  
### <a name="a-conditionally-executing-print-if-exists"></a>A. 有條件地執行列印 (IF EXISTS)  
 這個範例會利用 `PRINT` 陳述式，有條件地傳回訊息。  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. 建立及顯示字串  
 下列範例會將 `GETDATE` 函數的結果轉換成 `nvarchar` 資料類型，且會將它和 `PRINT` 傳回的常值文字串連起來。  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. 有條件地執行列印  
 這個範例會利用 `PRINT` 陳述式，有條件地傳回訊息。  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
### <a name="d-building-and-displaying-a-string"></a>D. 建立及顯示字串  
 下列範例會將 `GETDATE` 函數的結果轉換成 `nvarchar` 資料類型，且會將它和 `PRINT` 傳回的常值文字串連起來。  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  


