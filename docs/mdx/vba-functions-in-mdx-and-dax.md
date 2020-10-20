---
description: MDX 和 DAX 中的 VBA 函數
title: MDX 和 DAX 中的 VBA 函數 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dcbf0f0321ddc0c1959c4681c0b1dddf49c1aba
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192288"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函數


  本檔包含 MDX 所支援之 [Visual Basic for Applications](/office/vba/Language/Reference/functions-visual-basic-for-applications) 函式中所有可用 VBA 函數的交叉參考;此外，當 DAX 語言的功能等價時，此清單會包含附注。  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函數參考  
  
|函數名稱|支援|注意|  
|-------------------|---------------|-----------|  
|Abs|DAX、MDX||  
|Array|不支援||  
|Asc|僅限 MDX||  
|AscW|僅限 MDX||  
|Atn|僅限 MDX||  
|CallByName|不支援||  
|CBool|僅限 MDX||  
|CByte|僅限 MDX||  
|CCur|僅限 MDX||  
|CDate|僅限 MDX||  
|CDbl|僅限 MDX||  
|CDec|僅限 MDX||  
|Choose|僅限 MDX||  
|Chr|僅限 MDX||  
|CInt|僅限 MDX||  
|CLng|僅限 MDX||  
|CLngLng|不支援||  
|CLngPtr|不支援||  
|Command|不支援||  
|Cos|僅限 MDX||  
|CreateObject|不支援||  
|CSng|僅限 MDX||  
|CStr|僅限 MDX||  
|CurDir|不支援||  
|CVar|僅限 MDX||  
|CVErr|不支援||  
|Date|僅限 MDX|**警告** DAX 會使用相同的名稱來執行不同的函數;日期 (Year，Month，Day) 函數，用來從指定的引數產生日期類型值|  
|DateAdd|僅限 MDX|**警告** DAX 會使用相同的名稱來執行不同的函數;DATEADD (\<dates> ，<number_of_intervals>，) 函式 \<interval> ，用來將指定的日期移位指定的間隔數|  
|DateDiff|僅限 MDX||  
|DatePart|僅限 MDX||  
|DateSerial|僅限 MDX||  
|DateValue|DAX、MDX||  
|天|DAX、MDX||  
|DDB|僅限 MDX||  
|Dir|不支援||  
|DoEvents|不支援||  
|Environ|不支援||  
|EOF|不支援||  
|錯誤|不支援||  
|Exp|DAX、MDX||  
|FileAttr|不支援||  
|FileDateTime|不支援||  
|FileLen|不支援||  
|Filter|不支援|**警告** MDX 會實作為相同名稱的不同函數;篩選 (Set_Expression，Logical_Expression) 函式會根據指定引數中的搜尋條件，傳回根據搜尋條件篩選指定集合所產生的集合。<br /><br /> **警告** DAX 會使用相同的名稱來執行不同的函數;篩選 (\<table> ， \<filter>) 函數會從指定的引數傳回代表另一個資料表或運算式之子集的資料表。|  
|修正|僅限 MDX||  
|Format (Visual Basic for Applications)|DAX、MDX||  
|FormatCurrency|不支援||  
|FormatDateTime|不支援||  
|FormatNumber|不支援||  
|FormatPercent|不支援||  
|FreeFile|不支援||  
|FV|僅限 MDX||  
|GetAllSettings|不支援||  
|GetAttr|不支援||  
|GetObject|不支援||  
|GetSetting|不支援||  
|Hex|僅限 MDX||  
|小時|DAX、MDX||  
|Iif|僅限 MDX|**警告** DAX 會實作為名稱的類似函式：如果 (logical_test、value_if_true value_if_false) 函數。|  
|IMEStatus|不支援||  
|輸入|不支援||  
|InputBox|不支援||  
|InStr|僅限 MDX||  
|InStrRev|不支援||  
|Int|DAX、MDX||  
|IPmt|僅限 MDX||  
|IRR|僅限 MDX||  
|IsArray|僅限 MDX||  
|僅限 IsDateMDX||  
|IsEmpty|僅限 MDX||  
|IsError|DAX、MDX||  
|IsMissing|僅限 MDX||  
|IsNull|僅限 MDX||  
|IsNumeric|僅限 MDX||  
|IsObject|不支援||  
|Join|不支援||  
|LBound|不支援||  
|LCase|僅限 MDX||  
|Left|DAX、MDX||  
|Len|DAX、MDX||  
|Loc|不支援||  
|LOF|不支援||  
|Log|僅限 MDX|**重要** DAX 會使用相同的名稱來執行不同的函數;記錄 (編號，基底) 函數。 依照給定引數所指定的底數，傳回數字的對數。|  
|LTrim|僅限 MDX||  
|MacID|不支援||  
|MacScript|不支援||  
|Mid|DAX、MDX||  
|Minute|DAX、MDX||  
|MIRR|僅限 MDX||  
|Month|DAX、MDX||  
|MonthName|不支援||  
|MsgBox|不支援||  
|Now|DAX、MDX||  
|NPer|僅限 MDX||  
|NPV|僅限 MDX||  
|Oct|僅限 MDX||  
|資料分割|僅限 MDX||  
|Pmt|僅限 MDX||  
|PPmt|僅限 MDX||  
|PV|僅限 MDX||  
|QBColor|僅限 MDX||  
|費率|僅限 MDX||  
|取代|不支援||  
|RGB|僅限 MDX||  
|Right|DAX、MDX||  
|Rnd|僅限 MDX||  
|Round|DAX、MDX||  
|RTrim|僅限 MDX||  
|Second|DAX、MDX||  
|Seek|不支援||  
|Sgn|DAX、MDX||  
|殼層|不支援||  
|Sin|僅限 MDX||  
|SLN|僅限 MDX||  
|Space|僅限 MDX||  
|Spc|不支援||  
|分割|不支援||  
|Sqr|僅限 MDX||  
|Str|僅限 MDX||  
|StrComp|僅限 MDX||  
|StrConv|僅限 MDX||  
|String|僅限 MDX||  
|StrReverse|不支援||  
|參數|僅限 MDX||  
|SYD|僅限 MDX||  
|索引標籤|不支援||  
|Tan|僅限 MDX||  
|時間|不支援||  
|計時器|僅限 MDX||  
|TimeSerial|僅限 MDX||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|僅限 MDX||  
|UBound|不支援||  
|UCase|僅限 MDX||  
|Val|僅限 MDX||  
|VarType|不支援||  
|Weekday|DAX、MDX||  
|WeekdayName|不支援||  
|Year|DAX、MDX||  
  
