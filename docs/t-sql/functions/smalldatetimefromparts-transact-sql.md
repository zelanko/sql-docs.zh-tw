---
title: "SMALLDATETIMEFROMPARTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 0f561d37aae876f94946c8210665f642daec9755
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  傳回**smalldatetime**指定的日期和時間值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
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
  
## <a name="return-types"></a>傳回類型  
 **smalldatetime**  
  
## <a name="remarks"></a>備註  
 此函式作用類似的建構函式與完全初始化**smalldatetime**值。 如果引數無效，將會引發錯誤。 如果要求的引數為 null，即會傳回 null。  
  
 函數可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 不是從遠端處理到伺服器，在版本低於[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="examples"></a>範例  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  


