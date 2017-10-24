---
title: "開始...結束 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BEGIN
- BEGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1045a89eb41a7f84b4b2a2a5cbe305c67e776fb1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  含括一系列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，以便執行一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 BEGIN 和 END 是流程控制語言關鍵字。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>引數  
 { *q* | *statement_block* }  
 這是藉由使用陳述式區塊所定義的任何有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式分組。  
  
## <a name="remarks"></a>備註  
 BEGIN...END 區塊可以有巢狀結構。  
  
 雖然 BEGIN...END 區塊中所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式都是有效的陳述式，但某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式不應在同一批次或陳述式區塊中分成一組。  
  
## <a name="examples"></a>範例  
 在下列範例中，`BEGIN` 和 `END` 會定義一系列同時執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 如果沒有 `BEGIN...END` 區塊，這兩個 `ROLLBACK TRANSACTION` 陳述式都要執行，而且都會傳回這兩個 `PRINT` 訊息。  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 在下列範例中，`BEGIN`和`END`定義一系列的[!INCLUDE[DWsql](../../includes/dwsql-md.md)]一起執行的陳述式。 如果`BEGIN...END`區塊不會包含，下列範例會循環。  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [流程控制語言 &#40;TRANSACT-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [結束 &#40;開始...結束 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  



