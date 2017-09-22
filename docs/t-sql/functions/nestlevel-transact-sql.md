---
title: "@@NESTLEVEL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@NESTLEVEL'
- '@@NESTLEVEL_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@NESTLEVEL function'
- nesting stored procedures
- stored procedure nesting levels [SQL Server]
ms.assetid: 8c0b2134-8616-44f6-addc-6583c432fb62
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: d02995ee7093d311cbdc6f4b69430a8bc66a618c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40nestlevel-transact-sql"></a>（& s) #x 40; & #x 40。NESTLEVEL (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回本機伺服器中執行目前預存程序的巢狀層級 (最初是 0)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@NESTLEVEL  
```  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 每次預存程序呼叫另一個預存程序時，或參考 Common Language Runtime (CLR) 常式、類型或彙總來執行 Managed 程式碼時，巢狀層級都會遞增。 當到達最大值 32 時，交易便告終止。  
  
 當 @@NESTLEVEL內執行時[!INCLUDE[tsql](../../includes/tsql-md.md)]字串，則傳回值 1 + 目前的巢狀層級。 當 @@NESTLEVEL執行動態使用 sp_executesql 傳回的值是 2 + 目前的巢狀層級。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-nestlevel-in-a-procedure"></a>A. 使用@NESTLEVEL程序中  
 下列範例會建立兩個程序：一個程序呼叫另一個程序，一個程序顯示各程序的 `@@NESTLEVEL` 設定。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'usp_OuterProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_OuterProc;  
GO  
IF OBJECT_ID (N'usp_InnerProc', N'P')IS NOT NULL  
    DROP PROCEDURE usp_InnerProc;  
GO  
CREATE PROCEDURE usp_InnerProc AS   
    SELECT @@NESTLEVEL AS 'Inner Level';  
GO  
CREATE PROCEDURE usp_OuterProc AS   
    SELECT @@NESTLEVEL AS 'Outer Level';  
    EXEC usp_InnerProc;  
GO  
EXECUTE usp_OuterProc;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Outer Level`  
  
 `-----------`  
  
 `1`  
  
 `Inner Level`  
  
 `-----------`  
  
 `2`  
  
### <a name="b-calling-nestlevel"></a>B. 呼叫@NESTLEVEL  
 下列範例會顯示 `SELECT`、`EXEC` 和 `sp`_`executesql` 呼叫 `@@NESTLEVEL` 時，它們所傳回之值的差異。  
  
```  
CREATE PROC usp_NestLevelValues AS  
    SELECT @@NESTLEVEL AS 'Current Nest Level';  
EXEC ('SELECT @@NESTLEVEL AS OneGreater');   
EXEC sp_executesql N'SELECT @@NESTLEVEL as TwoGreater' ;  
GO  
EXEC usp_NestLevelValues;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Current Nest Level`  
  
 `------------------`  
  
 `1`  
  
 `(1 row(s) affected)`  
  
 `OneGreater`  
  
 `-----------`  
  
 `2`  
  
 `(1 row(s) affected)`  
  
 `TwoGreater`  
  
 `-----------`  
  
 `3`  
  
 `(1 row(s) affected)`  
  
## <a name="see-also"></a>另請參閱  
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
  

