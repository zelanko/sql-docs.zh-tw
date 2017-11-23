---
title: "TAN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TAN_TSQL
- TAN
dev_langs: TSQL
helpviewer_keywords:
- TAN function
- tangent
ms.assetid: f679fa6a-5739-484b-9450-fb3400d4f30c
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed751407c2274d7c9152fd7a4354acc61e613935
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="tan-transact-sql"></a>TAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回輸入運算式的正切函數 (Tangent)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TAN ( float_expression )  
```  
  
## <a name="arguments"></a>引數  
 *float_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)型別的**float**或可以隱含地轉換成的型別**float**，解譯為弧度的數目。  
  
## <a name="return-types"></a>傳回類型  
 **float**  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `PI()/2` 的正切函數 (Tangent)。  
  
```  
SELECT TAN(PI()/2);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------  
1.6331778728383844E+16  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回.45 的正切值。  
  
```  
SELECT TAN(.45);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
--------  
0.48
```  
  
## <a name="see-also"></a>請參閱＜  
 [數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

