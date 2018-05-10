---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5549f258e758cc91a228d5fee707120b57963d46
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回包含指定時差和精確度之指定日期和時間的 **datetimeoffset** 值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
指定分數的整數運算式。
  
*hour_offset*  
指定時區時差的小時部分之整數運算式。
  
*minute_offset*  
指定時區時差的分鐘部分之整數運算式。
  
*有效位數*  
此整數常值指定 **datetimeoffset** 傳回值的精確度。
  
## <a name="return-types"></a>傳回型別
**datetimeoffset(** *precision* **)**
  
## <a name="remarks"></a>Remarks  
**DATETIMEOFFSETFROMPARTS** 會傳回完整初始化的 **datetimeoffset** 資料類型。 位移引數可用以代表的時區時差。 如果省略位移引數，將會假設時區時差為 00:00，意即沒有時差。 如果指定了時差引數，則兩個引數都必須存在，且兩者皆必須為正數或負數。 若未搭配 *hour_offset* 指定 *minute_offset*，則便會引發錯誤。 如果其他引數無效，也將引發錯誤。 如果需要的引數為 Null，則傳回 Null。 然而，若 *precision* 引數為 Null，則會引發錯誤。
  
*fractions* 引數相依於 *precision* 引數。 例如，假設 *precision* 為 7，每個分數即表示 100 奈秒；如果 *precision* 為 3，每個分數即表示 1 毫秒。 如果 *precision* 的值為零，*fractions* 也必須為零，否則將引發錯誤。
  
函數可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 它在版本低於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的伺服器上無法以遠端方式運作。
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小數部分的簡單範例  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 含秒的小數部分的範例  
以下範例示範 *fractions* 和 *precision* 參數的用法：
1.   若 *fractions* 的值為 5、*precision* 的值為 1，則 *fractions* 的值表示 5/10 秒。  
1.   若 *fractions* 的值為 50、*precision* 的值為 2，則 *fractions* 的值表示 50/100 秒。  
1.   若 *fractions* 的值為 500、*precision* 的值為 3，則 *fractions* 的值表示 500/1000 秒。  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[AT TIME ZONE &#40;Transact-SQL&#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  


