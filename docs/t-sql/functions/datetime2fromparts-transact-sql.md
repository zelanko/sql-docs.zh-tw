---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce109671228e82bc0f02e9920b2ef98c9bbcdb83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

以指定的精確度傳回指定日期與時間的 **datetime2** 值。
  
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
  
*minute* 指定分鐘的整數運算式。
  
*seconds*  
指定秒的整數運算式。
  
*fractions*  
指定分數的整數運算式。
  
*有效位數*  
此整數常值指定 **datetime2** 傳回值的精確度。
  
## <a name="return-types"></a>傳回型別
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIME2FROMPARTS** 會傳回完整初始化的 **datetime2** 值。 如果引數無效，將會引發錯誤。 如果要求的引數為 null，即會傳回 null。 然而，若 *precision* 引數為 null，則會引發錯誤。
  
*fractions* 引數相依於 *precision* 引數。 例如，假設 *precision* 為 7，每個分數即表示 100 奈秒；如果 *precision* 為 3，每個分數即表示 1 毫秒。 如果 *precision* 的值為零，*fractions* 也必須為零，否則將引發錯誤。
  
函數可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 它在版本低於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的伺服器上無法以遠端方式運作。
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小數部分的簡單範例  
  
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
以下範例示範 *fractions* 和 *precision* 參數的用法：
  
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
  
  

