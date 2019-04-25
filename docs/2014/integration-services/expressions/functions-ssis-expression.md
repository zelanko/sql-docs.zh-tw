---
title: 函式 (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- expressions [Integration Services], functions
- string functions
- SQL Server Integration Services, functions
- SSIS, functions
ms.assetid: e9a41a31-94f4-46a4-b737-c707dd59ce48
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f70cde85aca7b08003d27ee3bd2fc61cbc0a45f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769124"
---
# <a name="functions-ssis-expression"></a>函數 (SSIS 運算式)
  運算式語言包含一組可在運算式中使用的函數。 運算式可使用單一函數，但通常運算式會結合函數與運算子，並使用多個函數。  
  
 函數可分類成下列各群組：  
  
-   數學函數，執行以做為函數參數的數字輸入值為主的運算並傳回數值。  
  
-   字串函數，執行字串和十六進位輸入值的運算，並傳回字串或數值。  
  
-   日期和時間函數，執行日期和時間值的運算，並傳回字串、數值或日期和時間值。  
  
-   系統函數，會傳回運算式的資訊。  
  
 運算式語言提供下列數學函數。  
  
|函數|描述|  
|--------------|-----------------|  
|[ABS &#40;SSIS 運算式&#41;](abs-ssis-expression.md)|傳回數值運算式的絕對正數值。|  
|[EXP &#40;SSIS 運算式&#41;](exp-ssis-expression.md)|傳回做為指定運算式中 e 之基底的指數。|  
|[CEILING &#40;SSIS 運算式&#41;](ceiling-ssis-expression.md)|傳回大於或等於數值運算式的最小整數。|  
|[FLOOR &#40;SSIS 運算式&#41;](floor-ssis-expression.md)|傳回小於或等於數值運算式的最大整數。|  
|[LN &#40;SSIS 運算式&#41;](ln-ssis-expression.md)|傳回數值運算式的自然對數。|  
|[LOG &#40;SSIS 運算式&#41;](log-ssis-expression.md)|傳回數值運算式以 10 為底的對數。|  
|[POWER &#40;SSIS 運算式&#41;](power-ssis-expression.md)|傳回數值運算式的乘冪結果。|  
|[ROUND &#40;SSIS 運算式&#41;](round-ssis-expression.md)|傳回已經進位到指定長度或有效位數的數值運算式。 .|  
|[SIGN &#40;SSIS 運算式&#41;](sign-ssis-expression.md)|傳回數值運算式的正 (+)、負 (-) 或零 (0) 符號。|  
|[SQUARE &#40;SSIS 運算式&#41;](square-ssis-expression.md)|傳回數值運算式的平方。|  
|[SQRT &#40;SSIS 運算式&#41;](sqrt-ssis-expression.md)|傳回數值運算式的平方根。|  
  
 運算式評估工具提供下列字串函數。  
  
|函數|描述|  
|--------------|-----------------|  
|[CODEPOINT &#40;SSIS 運算式&#41;](codepoint-ssis-expression.md)|傳回字元運算式最左邊字元的 Unicode 字碼值。|  
|[FINDSTRING &#40;SSIS 運算式&#41;](findstring-ssis-expression.md)|傳回運算式中，所指定字元字串出現位置的以 1 為基底的索引。|  
|[HEX &#40;SSIS 運算式&#41;](hex-ssis-expression.md)|傳回代表整數的十六進位值的字串。|  
|[LEN &#40;SSIS 運算式&#41;](len-ssis-expression.md)|傳回字元運算式中的字元數。|  
|[LEFT &#40;SSIS 運算式&#41;](left-ssis-expression.md)|傳回來自給定字元運算式最左邊部分的指定字元數。|  
|[LOWER &#40;SSIS 運算式&#41;](lower-ssis-expression.md)|傳回將大寫字元轉換為小寫字元之後的字元運算式。|  
|[LTRIM &#40;SSIS 運算式&#41;](trim-ssis-expression.md)|傳回移除開頭空白之後的字元運算式。|  
|[REPLACE &#40;SSIS 運算式&#41;](replace-ssis-expression.md)|以不同的字串或空白字串取代運算式中的字串後，傳回字元運算式。|  
|[REPLICATE &#40;SSIS 運算式&#41;](replicate-ssis-expression.md)|傳回重複了指定次數的字元運算式。|  
|[REVERSE &#40;SSIS 運算式&#41;](reverse-ssis-expression.md)|傳回反向順序的字元運算式。|  
|[RIGHT &#40;SSIS 運算式&#41;](right-ssis-expression.md)|傳回來自給定字元運算式最右邊部分的指定字元數。|  
|[RTRIM &#40;SSIS 運算式&#41;](rtrim-ssis-expression.md)|傳回移除尾端空白之後的字元運算式。|  
|[SUBSTRING &#40;SSIS 運算式&#41;](substring-ssis-expression.md)|傳回部份字元運算式。|  
|[TRIM &#40;SSIS 運算式&#41;](trim-ssis-expression.md)|傳回移除開頭和尾端空白之後的字元運算式。|  
|[UPPER &#40;SSIS 運算式&#41;](upper-ssis-expression.md)|傳回小寫字元轉換為大寫字元之後的字元運算式。|  
  
 運算式評估工具提供下列日期和時間函數。  
  
|函數|描述|  
|--------------|-----------------|  
|[DATEADD &#40;SSIS 運算式&#41;](dateadd-ssis-expression.md)|藉由將日期或時間間隔加入至指定的日期，傳回新的 DT_DBTIMESTAMP 值。|  
|[DATEDIFF &#40;SSIS 運算式&#41;](datediff-ssis-expression.md)|傳回跨越兩個指定日期的日期和時間界線數目。|  
|[DATEPART &#40;SSIS 運算式&#41;](datepart-ssis-expression.md)|傳回代表日期之日期部分的整數。|  
|[DAY &#40;SSIS 運算式&#41;](day-ssis-expression.md)|傳回代表指定日期中日部份的整數。|  
|[GETDATE &#40;SSIS 運算式&#41;](getdate-ssis-expression.md)|傳回系統目前的日期。|  
|[GETUTCDATE &#40;SSIS 運算式&#41;](getutcdate-ssis-expression.md)|傳回以 UTC 時間 (Universal Time Coordinate 或 Greenwich Mean Time) 表示的系統目前日期。|  
|[MONTH &#40;SSIS 運算式&#41;](month-ssis-expression.md)|傳回代表指定日期中月份的整數。|  
|[YEAR &#40;SSIS 運算式&#41;](year-ssis-expression.md)|傳回代表指定日期中年份的整數。|  
  
 運算式評估工具提供下列 Null 函數。  
  
|函數|描述|  
|--------------|-----------------|  
|[ISNULL &#40;SSIS 運算式&#41;](null-ssis-expression.md)|依據運算式是否為 Null 來傳回布林結果。|  
|[NULL &#40;SSIS 運算式&#41;](null-ssis-expression.md)|傳回所要求資料類型的 Null 值。|  
  
 運算式名稱會以大寫字元顯示，但運算式名稱不區分大小寫。 例如，使用「null」與使用「NULL」的功能相同。  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md)   
 [進階 Integration Services 運算式範例](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 運算式](integration-services-ssis-expressions.md)  
  
  
