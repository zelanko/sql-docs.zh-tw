---
title: "+ = （字串串連及指派） (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- concatenate strings
- string concatenation
- += (concatenate operator)
ms.assetid: 4aaeaab7-9b2b-48e0-8487-04ed672ebcb1
caps.latest.revision: "15"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1e42125e49b0191b4ccdcc3628b75d025cccb6a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="-string-concatenation-assignment-transact-sql"></a>+ = （字串串連指派） (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  串連兩個字串，並將該字串設定為運算結果。 例如，如果變數@x等於 'Adventure'，然後@x+ = 'Works' 會採用的原始值@x、 將 'Works' 加入到字串，並設定@x為該新值 'AdventureWorks'。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
expression += expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字元資料類型。  
  
## <a name="result-types"></a>結果類型  
 傳回針對變數所定義的資料類型。  
  
## <a name="remarks"></a>備註  
 設定@v1+ = 'expression' 相當於 SET @v1 = @v1 + ('expression')。 此外，設定@v1= @v2 + @v3 +@v4相當於 SET @v1 = (@v2 + @v3) + @v4。  
  
 += 運算子無法在沒有變數的情況下使用。 例如，下列程式碼將會造成錯誤：  
  
```  
SELECT 'Adventure' += 'Works'  
```  
  
## <a name="examples"></a>範例  
### <a name="a-concatenation-using--operator"></a>A. 串連使用 + = 運算子
 下列範例會使用 `+=` 運算子串連。  
  
```  
DECLARE @v1 varchar(40);  
SET @v1 = 'This is the original.';  
SET @v1 += ' More text.';  
PRINT @v1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `This is the original. More text.`  
  
### <a name="b-order-of-evaluation-while-concatenating-using--operator"></a>B. 當串連使用 + = 運算子的評估順序
下列範例串連多個字串來形成一個長字串，並嘗試計算最終的字串的長度。 此範例會示範使用串連運算子時評估順序和截斷規則。 

```
DECLARE @x varchar(4000) = replicate('x', 4000)
DECLARE @z varchar(8000) = replicate('z',8000)
DECLARE @y varchar(max);
 
SET @y = '';
SET @y += @x + @z;
SELECT LEN(@y) AS Y; -- 8000
 
SET @y = '';
SET @y = @y + @x + @z;
SELECT LEN(@y) AS Y; -- 12000
 
SET @y = '';
SET @y = @y +(@x + @z);
SELECT LEN(@y) AS Y; -- 8000
-- or
SET @y = '';
SET @y = @x + @z + @y;
SELECT LEN(@y) AS Y; -- 8000
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
    
 Y       
 ------- 
 12000 
  
 (1 row(s) affected) 

 Y       
 ------- 
 8000 
  
 (1 row(s) affected) 
  
 Y       
 ------- 
 8000 
  
 (1 row(s) affected)
  ```   
   
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [+ = &#40;新增指派 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [+ &#40;字串串連 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/string-concatenation-transact-sql.md)  
  
  
