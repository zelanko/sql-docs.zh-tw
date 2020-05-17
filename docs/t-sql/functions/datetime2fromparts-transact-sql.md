---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 400de28e3191b953c1f44dfdf0777678f031e140
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68119129"
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

此函式會傳回指定日期和時間引數的 **datetime2** 值。 傳回值具有 precision 引數所指定的精確度。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>引數  
*year*  
指定年份的整數運算式。
  
*month*  
指定月份的整數運算式。
  
*day*  
指定日期的整數運算式。
  
*hour*  
指定小時的整數運算式。
  
*minute*  
指定分鐘的整數運算式。
  
*seconds*  
指定秒的整數運算式。
  
*fractions*  
指定小數秒值的整數運算式。
  
*有效位數*  
整數運算式，指定 **會傳回之**datetime2`DATETIME2FROMPARTS` 值的精確度。
  
## <a name="return-types"></a>傳回類型
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>備註  
`DATETIME2FROMPARTS` 會傳回完整初始化的 **datetime2** 值。 如果至少一個必要引數具有無效的值，`DATETIME2FROMPARTS` 會引發錯誤。 如果至少一個必要引數具有 Null 值，則 `DATETIME2FROMPARTS` 會傳回 Null。 不過，如果 *precision* 引數為 Null 值，`DATETIME2FROMPARTS` 會引發錯誤。

*fractions* 引數相依於 *precision* 引數。 例如，*precision* 值為 7 的每個部分表示 100 奈秒；*precision* 為 3 的每個部分表示 1 毫秒。 如果 *precision* 值為零，*fractions* 也必須為零，否則 `DATETIME2FROMPARTS` 會引發錯誤。
  
此函式支援遠端處理到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器及更新版本。 它不支援遠端處理到版本低於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的伺服器。
  
## <a name="examples"></a>範例  
  
### <a name="a-an-example-without-fractions-of-a-second"></a>A. 不包含秒之小數部分的範例  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 含秒的小數部分的範例  
此範例示範 *fractions* 和 *precision* 參數的用法：
  
1.  若 *fractions* 的值為 5、*precision* 的值為 1，則 *fractions* 的值表示 5/10 秒。  
  
2.  若 *fractions* 的值為 50、*precision* 的值為 2，則 *fractions* 的值表示 50/100 秒。  
  
3.  若 *fractions* 的值為 500、*precision* 的值為 3，則 *fractions* 的值表示 500/1000 秒。  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

