---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab75a2147946366fba194f654a3710b32f68d626
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

為數學函數，可傳回指定數值運算式的絕對 (正) 值。 (`ABS` 會將負值變更為正值。 `ABS` 對零或正值沒有任何效果。)
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>引數  
*numeric_expression*  
精確數值或近似數值資料型別類別目錄的運算式。
  
## <a name="return-types"></a>傳回類型  
傳回與 *numeric_expression*相同的類型。
  
## <a name="examples"></a>範例  
此範例顯示在三個不同數字上使用 `ABS` 函數的結果。
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
當數字的絕對值超過所指定資料型別能表示的最大數字時，`ABS` 函數可能會產生溢位錯誤。 例如，`int` 資料型別值的範圍在 `-2,147,483,648` 到 `2,147,483,647`。 計算帶正負號整數 `-2,147,483,648` 的絕對值會造成溢位錯誤，因為其絕對值超過 `int` 資料型別的正數範圍限制。
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
傳回此錯誤訊息：
  
「訊息 8115，層級 16，狀態 2，行 3」
  
「轉換運算式到資料類型 int 時發生算術溢位錯誤。」

  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[內建函數 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

