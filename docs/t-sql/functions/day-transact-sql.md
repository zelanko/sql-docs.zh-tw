---
title: DAY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/30/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 444df60a2cfe3adae045020b3db8d673946dccb1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回代表指定 *date* 之日 (月份中的日期) 的整數。
  
如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函式的概觀，請參閱[日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>引數  
*date*  
為可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2**，或 **datetimeoffset** 值的運算式。 *date* 引數可以是運算式、資料行運算式、使用者定義變數或字串常值。
  
## <a name="return-type"></a>傳回類型  
**int**
  
## <a name="return-value"></a>傳回值  
DAY 會與 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**day**, *date*) 傳回相同的值。
  
如果 *date* 僅包含時間部分，傳回值就是 1 (基底日期)。
  
## <a name="examples"></a>範例  
下列陳述式會傳回 `30`。 這是日數。
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
下列陳述式會傳回 `1900, 1, 1`。 *date* 的引數是數字 `0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


