---
title: 參數 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- user-defined functions [SQL Server], parameters
ms.assetid: c1f9bd93-3271-4098-a23b-7bd7a19ab65b
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4b4b25665c3fdefc780533e3a38917f36b92a678
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560068"
---
# <a name="parameters"></a>參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
參數是用以交換預存程序和呼叫預存程序的函數、應用程式或工具之間的資料： 

*  輸入參數可讓呼叫者將資料值傳遞給預存程序或函數。
*  輸出參數可讓預存程序將資料值或資料指標變數傳回給呼叫者。 使用者自訂函數無法指定輸出參數。
*  每個預存程序傳回一個整數傳回碼給呼叫者。 如果預存程序沒有明確設定傳回碼的值，傳回碼為 0。

下列的預存程序範例中將顯示輸入參數、輸出參數和傳回碼 (Return Code) 的使用方式：
```
-- Create a procedure that takes one input parameter and returns one output parameter and a return code.
CREATE PROCEDURE SampleProcedure @EmployeeIDParm INT,
         @MaxTotal INT OUTPUT
AS
-- Declare and initialize a variable to hold @@ERROR.
DECLARE @ErrorSave INT
SET @ErrorSave = 0

-- Do a SELECT using the input parameter.
SELECT FirstName, LastName, JobTitle
FROM HumanResources.vEmployee
WHERE EmployeeID = @EmployeeIDParm

-- Save any nonzero @@ERROR value.
IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Set a value in the output parameter.
SELECT @MaxTotal = MAX(TotalDue)
FROM Sales.SalesOrderHeader;

IF (@@ERROR <> 0)
   SET @ErrorSave = @@ERROR

-- Returns 0 if neither SELECT statement had an error; otherwise, returns the last error.
RETURN @ErrorSave
GO
```

當執行預存程序或函數時，輸入參數可以將其值設為常數或使用變數的值。 輸出參數與傳回碼必須將其值傳回給變數。 參數和傳回碼可以和 Transact-SQL 變數或應用程式變數交換資料值。

如果是從批次或指令碼呼叫預存程序，參數和傳回碼值可以使用相同批次所定義的 Transact-SQL 變數。 下列範例是執行先前所建立的程序之批次。 輸入參數是指定為參數，而輸出參數和傳回碼將其值放置在 Transact-SQL 變數中：
```
-- Declare the variables for the return code and output parameter.
DECLARE @ReturnCode INT
DECLARE @MaxTotalVariable INT

-- Execute the stored procedure and specify which variables
-- are to receive the output parameter and return code values.
EXEC @ReturnCode = SampleProcedure @EmployeeIDParm = 19,
   @MaxTotal = @MaxTotalVariable OUTPUT

-- Show the values returned.
PRINT ' '
PRINT 'Return code = ' + CAST(@ReturnCode AS CHAR(10))
PRINT 'Maximum Quantity = ' + CAST(@MaxTotalVariable AS CHAR(10))
GO
```

應用程式可使用繫結至程式變數的參數標記，交換應用程式變數、參數和傳回碼間的資料。

## <a name="see-also"></a>另請參閱
[CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [CREATE FUNCTION (Transact-SQL)](../../t-sql/statements/create-function-transact-sql.md)   
 [參數和執行計畫的重複使用一節](../../relational-databases/query-processing-architecture-guide.md)   
 [變數 (Transact-SQL)](../../t-sql/language-elements/variables-transact-sql.md)
