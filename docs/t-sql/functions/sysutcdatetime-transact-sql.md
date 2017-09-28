---
title: "SYSUTCDATETIME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/01/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSUTCDATETIME
- SYSUTCDATETIME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- system time [SQL Server]
- functions [SQL Server], date and time
- time [SQL Server], functions
- date and time [SQL Server], SYSUTCDATETIME
- SYSUTCDATETIME function [SQL Server]
- time [SQL Server], system
ms.assetid: f14fc2cd-9ea8-4daf-88f4-418cf523ab55
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9dfaf40ac3d7722c39592fc3e7b4d4e790ec25f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="sysutcdatetime-transact-sql"></a>SYSUTCDATETIME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回**datetime2**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 以 UTC 時間 （國際標準時間） 傳回的日期和時間。 毫秒的有效位數規格範圍介於 1 至 7 位數之間。 預設有效位數是 7 位數。  
  
> [!NOTE]  
>  SYSDATETIME 和 SYSUTCDATE 比 GETDATE 和 GETUTCDATE 具有更多小數秒數有效位數。 SYSDATETIMEOFFSET 包含系統時區位移。 SYSDATETIME、SYSUTCDATE 和 SYSDATETIMEOFFSET 可指派給任何日期和時間類型的變數。  
  
 如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料類型與函數](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SYSUTCDATETIME ( )  
```  
  
## <a name="return-type"></a>傳回類型  
 **datetime2**  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式可以參考 SYSUTCDATETIME 任何位置，它們可以參考**datetime2**運算式。  
  
 SYSUTCDATETIME 是不具決定性的函數。 在資料行中參考這個函數的檢視表和運算式無法編製索引。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 GetSystemTimeAsFileTime() Windows API 來取得日期和時間值。 精確度取決於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦硬體和 Windows 版本。 此 API 的精確度是固定於 100 奈秒。 使用 GetSystemTimeAdjustment() Windows API，可判斷精確度。  
  
## <a name="examples"></a>範例  
 下列範例會使用六個可傳回目前日期和時間的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統函數來傳回日期、時間或這兩者。 由於這些值會依序傳回，因此其小數秒數可能會不同。  
  
### <a name="a-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>A. 顯示日期和時間函數所傳回的格式  
 下列範例示範日期和時間函數所傳回的不同格式。  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
### <a name="b-converting-date-and-time-to-date"></a>B. 將日期和時間轉換成日期  
 下列範例會顯示如何將日期和時間值轉換成 `date`。  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="c-converting-date-and-time-values-to-time"></a>C. 將日期和時間值轉換成時間  
 下列範例會顯示如何將日期和時間值轉換成 `time`。  
  
 `DECLARE @DATETIME DATETIME = GetDate();`  
  
 `DECLARE @TIME TIME`  
  
 `SELECT @TIME = CONVERT(time, @DATETIME)`  
  
 `SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Time             Date Time`  
  
 `13:49:33.6330000 2009-04-22 13:49:33.633`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會使用六個可傳回目前日期和時間的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統函數來傳回日期、時間或這兩者。 由於這些值會依序傳回，因此其小數秒數可能會不同。  
  
### <a name="d-showing-the-formats-that-are-returned-by-the-date-and-time-functions"></a>D. 顯示日期和時間函數所傳回的格式  
 下列範例示範日期和時間函數所傳回的不同格式。  
  
```  
SELECT SYSDATETIME() AS SYSDATETIME  
    ,SYSDATETIMEOFFSET() AS SYSDATETIMEOFFSET  
    ,SYSUTCDATETIME() AS SYSUTCDATETIME  
    ,CURRENT_TIMESTAMP AS CURRENT_TIMESTAMP  
    ,GETDATE() AS GETDATE  
    ,GETUTCDATE() AS GETUTCDATE;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `SYSDATETIME()      2007-04-30 13:10:02.0474381`  
  
 `SYSDATETIMEOFFSET()2007-04-30 13:10:02.0474381 -07:00`  
  
 `SYSUTCDATETIME()   2007-04-30 20:10:02.0474381`  
  
 `CURRENT_TIMESTAMP  2007-04-30 13:10:02.047`  
  
 `GETDATE()          2007-04-30 13:10:02.047`  
  
 `GETUTCDATE()       2007-04-30 20:10:02.047`  
  
### <a name="e-converting-date-and-time-to-date"></a>E. 將日期和時間轉換成日期  
 下列範例會顯示如何將日期和時間值轉換成 `date`。  
  
```  
SELECT CONVERT (date, SYSDATETIME())  
    ,CONVERT (date, SYSDATETIMEOFFSET())  
    ,CONVERT (date, SYSUTCDATETIME())  
    ,CONVERT (date, CURRENT_TIMESTAMP)  
    ,CONVERT (date, GETDATE())  
    ,CONVERT (date, GETUTCDATE());  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
 `2007-04-30`  
  
### <a name="f-converting-date-and-time-values-to-time"></a>F. 將日期和時間值轉換成時間  
 下列範例會顯示如何將日期和時間值轉換成 `time`。  
  
 `DECLARE @DATETIME DATETIME = GetDate();`  
  
 `DECLARE @TIME TIME`  
  
 `SELECT @TIME = CONVERT(time, @DATETIME)`  
  
 `SELECT @TIME AS 'Time', @DATETIME AS 'Date Time'`  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Time             Date Time`  
  
 `13:49:33.6330000 2009-04-22 13:49:33.633`  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [日期和時間資料類型和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)   
 [TIME ZONE &AMP; #40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)  
  
  



