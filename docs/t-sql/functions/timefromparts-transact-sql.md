---
title: "TIMEFROMPARTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs: TSQL
helpviewer_keywords: TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5e046e203e7ebd5243cdfc6f10948dfd353b2dd3
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  傳回**時間**針對指定的時間並使用指定的有效位數的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>引數  
 *小時*  
 指定小時的整數運算式。  
  
 *分鐘*  
 指定分鐘的整數運算式。  
  
 *seconds*  
 指定秒的整數運算式。  
  
 *分數*  
 指定分數的整數運算式。  
  
 *有效位數*  
 指定的有效位數的整數常值**時間**會傳回值。  
  
## <a name="return-types"></a>傳回類型  
 **時間 (** *精確度* **)**  
  
## <a name="remarks"></a>備註  
 TIMEROMPARTS 會傳回完整初始化的時間值。 如果引數無效，將會引發錯誤。 如有任何參數為 null，會傳回 null。 不過，如果*精確度*引數為 null，則會引發錯誤。  
  
 *分數*引數取決於*精確度*引數。 例如，如果*精確度*為 7，則每個分數即表示 100 奈秒; 如果*精確度*為 3，則每個分數即表示 1 毫秒。 如果值*精確度*是零，則值*分數*也必須為零，否則會引發錯誤。  
  
 這個函數可以遠端處理到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本的伺服器。 它無法遠端處理到版本低於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的伺服器。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小數部分的簡單範例  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 含秒的小數部分的範例  
 下列範例示範如何使用*分數*和*精確度*參數：  
  
1.  當*分數*的值為 5 和*精確度*然後的值具有值為 1，*分數*代表 5/10 秒。  
  
2.  當*分數*的值為 50 和*精確度*然後的值具有值為 2，*分數*表示 50/100 的第二個。  
  
3.  當*分數*的值為 500 和*精確度*然後的值具有值為 3，*分數*表示 500/1000 秒。  
  
```sql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  

