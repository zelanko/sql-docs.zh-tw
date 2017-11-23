---
title: "結束 （開始...結束） (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- END
- END_TSQL
dev_langs: TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- END keyword
- BEGIN...END keyword
- END (BEGIN...END) keyword
ms.assetid: 354c4935-1375-4141-8195-61326662f4d2
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e15aaa9fc6d4ea9b3c8a3c8b89826c85f0a4810f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="end-beginend-transact-sql"></a>END (BEGIN...END) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  含括將以群組方式來執行的序列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 BEGIN...END 區塊可以有巢狀結構。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
BEGIN   
     { sql_statement | statement_block }   
END   
```  
  
## <a name="arguments"></a>引數  
 { *q*| *statement_block*}  
 這是利用陳述式區塊來定義的任何有效 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或陳述式分組。 若要定義陳述式區塊 (批次)，請使用流程控制語言關鍵字 BEGIN 和 END。 雖然 BEGIN...END 區塊中所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式都是有效的，但某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式不應在同一批次 (陳述式區塊) 中群組在一起。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [開始...結束 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [流程控制語言 &#40;TRANSACT-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [其他 &#40; 如果...其他 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/else-if-else-transact-sql.md)   
 [如果...其他 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  


