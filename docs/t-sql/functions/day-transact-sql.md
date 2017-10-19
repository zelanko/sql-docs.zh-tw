---
title: "日 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 9edfdc46ede4c090080c09253e2bb213a384816c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回整數，代表指定之日期 （月份的天數）*日期*。
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>引數  
*date*  
運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*引數可以是運算式、 資料行運算式、 使用者定義變數或字串常值。
  
## <a name="return-type"></a>傳回類型  
**int**
  
## <a name="return-value"></a>傳回值  
DAY 會傳回相同的值[DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**天**，*日期*)。
  
如果*日期*僅包含時間部分，傳回值是 1，基底日期。
  
## <a name="examples"></a>範例  
下列陳述式會傳回 `30`。 這是日數。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
下列陳述式會傳回 `1900, 1, 1`。 引數*日期*是數字`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



