---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f9ef67d87b628f53b9bb97d6cf32ecb79aa3befb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  以選擇性位移，傳回包含指定日期的當月最後一天。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>引數  
 *start_date*  
 日期運算式為當月最後一天該傳回者指定日期。  
  
 *month_to_add*  
 指定要新增至 *start_date* 之月數的選擇性整數運算式。  
  
 如果已指定這個引數，則 **EOMONTH** 會將指定月數新增到 *start_date*，然後傳回當月最後一天作為結果日期。 如果這個加法溢位有效日期範圍，則會引起錯誤。  
  
## <a name="return-type"></a>傳回類型  
 **date**  
  
## <a name="remarks"></a>Remarks  
 這個函數可以遠端處理到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本的伺服器。 它無法遠端處理到版本低於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的伺服器。  
  
## <a name="examples"></a>範例  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. 具明確日期時間類型的 EOMONTH  
  
```  
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. 具有字串參數及明確轉換的 EOMONTH  
  
```  
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-monthtoadd-parameter"></a>C. 具有和不具有 month_to_add 參數的 EOMONTH  
  
```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```  
  
  

