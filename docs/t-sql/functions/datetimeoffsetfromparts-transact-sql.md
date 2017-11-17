---
title: "DATETIMEOFFSETFROMPARTS (TRANSACT-SQL) |Microsoft 文件"
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 665607c3b6ea9411d90137fba416d96d3d46a4c1
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回**datetimeoffset**具有指定的時差和精確度及指定的日期和時間值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
```  
  
## <a name="arguments"></a>引數  
*年份*  
指定年份的整數運算式。
  
*月份*  
指定月份的整數運算式。
  
*一天*  
指定日期的整數運算式。
  
*小時*  
指定小時的整數運算式。
  
*分鐘*  
指定分鐘的整數運算式。
  
*seconds*  
指定秒的整數運算式。
  
*分數*  
指定分數的整數運算式。
  
*hour_offset*  
指定時區時差的小時部分之整數運算式。
  
*minute_offset*  
指定時區時差的分鐘部分之整數運算式。
  
*有效位數*  
指定的有效位數的整數常值**datetimeoffset**會傳回值。
  
## <a name="return-types"></a>傳回型別
**datetimeoffset (** *精確度* **)**
  
## <a name="remarks"></a>備註  
**DATETIMEOFFSETFROMPARTS**傳回完整初始化**datetimeoffset**資料型別。 位移引數可用以代表的時區時差。 如果省略位移引數，將會假設時區時差為 00:00，意即沒有時差。 如果指定了時差引數，則兩個引數都必須存在，且兩者皆必須為正數或負數。 如果*minute_offset*指定不含*hour_offset*，則會引發錯誤。 如果其他引數無效，也將引發錯誤。 如果需要的引數為 Null，則傳回 Null。 不過，如果*精確度*引數為 null，則會引發錯誤。
  
*分數*引數取決於*精確度*引數。 例如，如果*精確度*為 7，則每個分數即表示 100 奈秒; 如果*精確度*為 3，則每個分數即表示 1 毫秒。 如果值*精確度*是零，則值*分數*也必須為零，否則會引發錯誤。
  
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
下列範例示範如何使用*分數*和*精確度*參數：
1.   當*分數*的值為 5 和*精確度*然後的值具有值為 1，*分數*代表 5/10 秒。  
1.   當*分數*的值為 50 和*精確度*然後的值具有值為 2，*分數*表示 50/100 的第二個。  
1.   當*分數*的值為 500 和*精確度*然後的值具有值為 3，*分數*表示 500/1000 秒。  
  
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
[TIME ZONE &AMP;#40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  



