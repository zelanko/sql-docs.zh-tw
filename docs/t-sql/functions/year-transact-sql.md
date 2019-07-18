---
title: YEAR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a8c6728692e27a1af301e28f58c9f3640d5eb48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944915"
---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回代表指定 *date* 中年份的整數。  
  
 如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函數的概觀，請參閱[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>引數  
 *date*  
 這是可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset** 值的運算式。 *date* 引數可以是運算式、資料行運算式、使用者定義變數或字串常值。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
 YEAR 會傳回與 [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**year**, *date*) 相同的值。  
  
 如果 *date* 僅包含時間部分，傳回值就是 1900 (基底年份)。  
  
## <a name="examples"></a>範例  
 下列陳述式會傳回 `2010`。 這是年份。  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 下列陳述式會傳回 `1900, 1, 1`。 *date* 的引數是數字 `0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列陳述式會傳回 `1900, 1, 1`。 *date* 的引數是數字 `0`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 `0` 解譯為 1900 年 1 月 1 日。  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

