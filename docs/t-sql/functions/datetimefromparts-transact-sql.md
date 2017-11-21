---
title: "DATETIMEFROMPARTS (TRANSACT-SQL) |Microsoft 文件"
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
- DATETIMEFROMPARTS_TSQL
- DATETIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEFROMPARTS function
ms.assetid: 6008148b-bf75-4c98-9392-68a89fa0711c
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 12c4107410cb0c482a24e40622d1858be9f7d1b2
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="datetimefromparts-transact-sql"></a>DATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回**datetime**指定的日期和時間值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATETIMEFROMPARTS ( year, month, day, hour, minute, seconds, milliseconds )  
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
  
*（毫秒)*  
指定毫秒的整數運算式。
  
## <a name="return-types"></a>傳回型別
**datetime**
  
## <a name="remarks"></a>備註  
**DATETIMEFROMPARTS**傳回完整初始化**datetime**值。 如果引數無效，將會引發錯誤。 如果需要的引數為 Null，則傳回 Null。
  
函數可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 它在版本低於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的伺服器上無法以遠端方式運作。
  
## <a name="examples"></a>範例  
  
```sql
SELECT DATETIMEFROMPARTS ( 2010, 12, 31, 23, 59, 59, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[日期時間 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)
  
  


