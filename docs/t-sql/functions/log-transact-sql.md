---
title: "記錄檔 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 7918cb0d2832e88f3e4218b98c7f606f559f2e4e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定的自然對數**float**中的運算式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>引數  
 *float_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)型別的**float**或可以隱含地轉換成的型別**float**。  
  
 *基底*  
 可設定對數基數的選擇性整數引數。  
  
**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
## <a name="return-types"></a>傳回類型  
 **float**  
  
## <a name="remarks"></a>備註  
 根據預設， **LOG**傳回自然對數。 從開始[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，您也可以使用選擇性另一個值來變更對數的基底*基底*參數。  
  
 自然對數是底數的對數**e**，其中**e**是大約等於 2.718281828 的無理常數。  
  
 自然對數的指數的數字是數字本身： 記錄檔 (EXP (  *n*  )) =  *n* 。 而數字的自然對數的指數是該數值本身： EXP (記錄檔 (  *n*  )) =  *n* 。  
  
## <a name="examples"></a>範例  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. 計算數值的對數。  
 下列範例會計算`LOG`指定**float**運算式。  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. 計算數值之指數的對數。  
 下列範例會計算一個數值之指數的 `LOG`。  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. 計算數字的對數  
 下列範例會計算`LOG`指定**float**運算式。  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>另請參閱  
 [數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40;TRANSACT-SQL &#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  


