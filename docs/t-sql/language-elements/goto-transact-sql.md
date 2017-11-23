---
title: "GOTO (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs: TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 9dbabcc0fe5f9573554384549023ab8395b87762
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="goto-transact-sql"></a>GOTO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將執行流程變更到標籤。 略過一或多個遵照 GOTO 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，從標籤開始繼續處理。 程序、批次或陳述式區塊內的任何位置，都可以使用 GOTO 陳述式。 GOTO 陳述式可以有巢狀結構。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
## <a name="arguments"></a>引數  
 *標籤*  
 這是 GOTO 的目標標籤，處理程序在這個點之後開始。 標籤必須遵循的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 標籤可用來作為是使用 GOTO 的註解化方法。  
  
## <a name="remarks"></a>備註  
 GOTO 可以在條件式流程控制陳述式、陳述式區塊或程序內，但它不能移至批次之外的標籤。 GOTO 分支可以移至定義在 GOTO 之前或之後的標籤。  
  
## <a name="permissions"></a>Permissions  
 GOTO 權限預設會授與任何有效的使用者。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何使用 `GOTO` 做為分支機制。  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>請參閱＜  
 [流程控制語言 &#40;TRANSACT-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [開始...結束 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [中斷 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [繼續 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [如果...其他 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
