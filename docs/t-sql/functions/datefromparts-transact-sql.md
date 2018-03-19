---
title: DATEFROMPARTS (Transact-SQL) | Microsoft Docs
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
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 73d2edfd6f0d19c4383b0bdbe1271d74a0ef2b6f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回指定之年、月、日的 **date** 值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>引數  
*year*  
指定年份的整數運算式。
  
*month*  
指定月份的整數運算式，從 1 到 12。
  
*day*  
指定日期的整數運算式。
  
## <a name="return-types"></a>傳回型別
**date**
  
## <a name="remarks"></a>Remarks  
**DATEFROMPARTS** 會傳回 **date** 值，其中日期部分會設為指定的年、月、日，而時間部分則會設為預設值。 如果引數無效，將會引發錯誤。 如果要求的引數為 null，即會傳回 null。
  
函數可以在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 它在版本低於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的伺服器上無法以遠端方式運作。
  
## <a name="examples"></a>範例  
以下範例示範 **DATEFROMPARTS** 函式。
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[日期 &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  

