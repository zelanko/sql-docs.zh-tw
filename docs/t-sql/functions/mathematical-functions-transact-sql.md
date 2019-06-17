---
title: 數學函式 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3a317cdb9e88696a26edb1355ea035dfe2cfb048
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65949095"
---
# <a name="mathematical-functions-transact-sql"></a>數學函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列純量函數會執行計算 (通常是以引數所提供的輸入值為基礎)，並傳回數值：  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[DEGREES](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[ROUND](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[SIGN](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[LOG](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[CEILING](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[SQUARE](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[POWER](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[RADIANS](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  ABS、CEILING、DEGREES、FLOOR、POWER、RADIANS 和 SIGN 等算術函數，會傳回資料類型與輸入值相同的值。 三角和其他函式 (包括 EXP、LOG、LOG10、SQUARE 和 SQRT) 會將它們的輸入值轉換成 **float** 及傳回 **float** 值。  
  
 除了 RAND，所有數學函數都是具決定性的函數。 這表示每次利用一組特定輸入值來呼叫它們時，都會傳回相同的結果。 只有在指定了初始參數時，RAND 才具決定性。 如需函數確定性的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另請參閱  
  [算術運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  
