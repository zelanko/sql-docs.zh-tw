---
title: ACOS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 42132bf92af16aedcd82581c1b658623da5f6df1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

為數學函式，它會傳回其餘弦函式為指定 **float** 運算式的角度 (以弧度為單位)；也稱為反餘弦函式。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ACOS ( float_expression )  
```  
  
## <a name="arguments"></a>引數  
*float_expression*  
為 **float** 類型或能夠隱含轉換成 **float** 之類型的運算式，值的範圍從 -1 到 1。 超出這個範圍的值會傳回 NULL 並且回報網域錯誤。
  
## <a name="return-types"></a>傳回類型  
**float**
  
## <a name="examples"></a>範例  
下列範例會傳回指定之數字的 ACOS。
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
### <a name="includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 

下列範例會傳回指定之數字的 ACOS。
  
```sql
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[數學函式 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[函數](../../t-sql/functions/functions.md)
  
  

