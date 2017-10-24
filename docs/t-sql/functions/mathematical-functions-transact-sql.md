---
title: "數學函數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec4a6767acab606d6459b439683a88a0cae1caf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mathematical-functions-transact-sql"></a>數學函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  下列純量函數會執行計算 (通常是以引數所提供的輸入值為基礎)，並傳回數值：  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[度](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[圓形](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[符號](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[記錄檔](../../t-sql/functions/log-transact-sql.md)|[SIN](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[CEILING](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[正方形](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[電源](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[弧度為單位](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  ABS、CEILING、DEGREES、FLOOR、POWER、RADIANS 和 SIGN 等算術函數，會傳回資料類型與輸入值相同的值。 三角和其他功能，包括 EXP、 記錄、 LOG10、 SQUARE 和 SQRT、 轉型到其輸入的值**float**並傳回**float**值。  
  
 除了 RAND，所有數學函數都是具決定性的函數。 這表示每次利用一組特定輸入值來呼叫它們時，都會傳回相同的結果。 只有在指定了初始參數時，RAND 才具決定性。 如需函數決定論的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="see-also"></a>另請參閱  
  [算術運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

