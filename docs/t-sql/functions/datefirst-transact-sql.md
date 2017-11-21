---
title: "@@DATEFIRST (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
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
- DATE_FORMAT_TSQL
- DATE FORMAT
- '@@DATEFIRST_TSQL'
- '@@DATEFIRST'
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], SET DATEFIRST
- first day of week [SQL Server]
- dates [SQL Server], first day of week
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- date and time [SQL Server], DATEFIRST
- DATEFIRST option [SQL Server]
- date and time [SQL Server], @@DATEFIRST
- weekdays [SQL Server]
- '@@DATEFIRST function [SQL Server]'
- functions [SQL Server], date and time
- options [SQL Server], date
ms.assetid: a178868e-49d5-4bd5-a5e2-1283409c8ce6
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 2dfe63f2d59cb3e3a1b563d524693af0d3dd1b51
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40datefirst-transact-sql"></a>&#x40;&#x40; DATEFIRST (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回目前的值，工作階段， [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)。
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```
@@DATEFIRST  
```  
  
## <a name="return-type"></a>傳回類型  
**tinyint**
  
## <a name="remarks"></a>備註  
SET DATEFIRST 會指定每週第一天。 U.S.English 預設值是 7，也就是星期日。
  
這個語言設定會影響字元字串轉換成日期值以便儲存在資料庫中的解譯方式，以及儲存在資料庫中之日期值的顯示。 這項設定不會影響日期資料的儲存格式。 在下列範例中，語言會先設定為 `Italian`。 陳述式 `SELECT @@DATEFIRST;` 會傳回 `1`。 然後，語言便設定為 `us_english`。 陳述式 `SELECT @@DATEFIRST;` 會傳回 `7`。
  
```sql
SET LANGUAGE Italian;  
GO  
SELECT @@DATEFIRST;  
GO  
SET LANGUAGE us_english;  
GO  
SELECT @@DATEFIRST;  
```  
  
## <a name="examples"></a>範例  
下列範例是將當週第一天設為 `5` (星期五)，並且假設當日 (`Today`) 是星期六。 `SELECT` 陳述式會傳回 `DATEFIRST` 值以及當週當日的號碼。
  
```sql
SET DATEFIRST 5;  
SELECT @@DATEFIRST AS 'First Day'  
    ,DATEPART(dw, SYSDATETIME()) AS 'Today';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
First Day         Today  
----------------  --------------  
5                 2  
```  
  
## <a name="example"></a>範例
 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT @@DATEFIRST;  
```  
  
## <a name="see-also"></a>另請參閱
[組態函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)
  
  


