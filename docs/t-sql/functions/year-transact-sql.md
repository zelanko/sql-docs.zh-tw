---
title: "年份 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 80a38599ae04209d0f8e479b8cbad16d39bef31a
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回一個整數，代表指定年份*日期*。  
  
 如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>引數  
 *date*  
 運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*引數可以是運算式、 資料行運算式、 使用者定義變數或字串常值。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
 YEAR 會傳回相同的值[DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**年**，*日期*)。  
  
 如果*日期*僅包含時間部分，則傳回值是 1900 年基底年份。  
  
## <a name="examples"></a>範例  
 下列陳述式會傳回 `2010`。 這是年份。  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 下列陳述式會傳回 `1900, 1, 1`。 引數*日期*是數字`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列陳述式會傳回 `1900, 1, 1`。 引數*日期*是數字`0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


