---
title: MDX 和 DAX 中的 VBA 函數 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135024"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函數


  本檔包含 MDX 中支援之[Visual Basic for Applications](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications)函式內所有可用 VBA 函式的交叉參考;此外，當 DAX 語言的功能等價時，此清單也會包含附注。  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函數參考  
  
|函數名稱|支援|注意|  
|-------------------|---------------|-----------|  
|Abs|DAX、MDX||  
|Array|不受支援||  
|Asc|僅限 MDX||  
|AscW|僅限 MDX||  
|Atn|僅限 MDX||  
|CallByName|不受支援||  
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
|CLngLng|不受支援||  
|CLngPtr|不受支援||  
|Command|不受支援||  
|Cos|僅限 MDX||  
|CreateObject|不受支援||  
|CSng|僅限 MDX||  
|CStr|僅限 MDX||  
|CurDir|不受支援||  
|CVar|僅限 MDX||  
|CVErr|不受支援||  
|Date|僅限 MDX|**警告**DAX 會使用相同的名稱來執行不同的函式;日期（年、月、日）函數，用來從指定的引數產生日期類型值|  
|DateAdd|僅限 MDX|**警告**DAX 會使用相同的名稱來執行不同的函式;DATEADD （\<日期>，<number_of_intervals>，\<interval>）函式，用來依指定的間隔數來位移指定的日期|  
|DateDiff|僅限 MDX||  
|DatePart|僅限 MDX||  
|DateSerial|僅限 MDX||  
|DateValue|DAX、MDX||  
|Day|DAX、MDX||  
|DDB|僅限 MDX||  
|Dir|不受支援||  
|DoEvents|不受支援||  
|Environ|不受支援||  
|EOF|不受支援||  
|錯誤|不受支援||  
|Exp|DAX、MDX||  
|FileAttr|不受支援||  
|FileDateTime|不受支援||  
|FileLen|不受支援||  
|Filter|不受支援|**警告**MDX 會使用相同的名稱來執行不同的函式;FILTER （Set_Expression，Logical_Expression）函數會根據指定引數中的搜尋條件，傳回從篩選指定集合所產生的集合。<br /><br /> **警告**DAX 會使用相同的名稱來執行不同的函式;篩選（\<資料表>、\<篩選>）函數會從指定的引數傳回代表另一個資料表或運算式之子集的資料表|  
|修正|僅限 MDX||  
|Format (Visual Basic for Applications)|DAX、MDX||  
|FormatCurrency|不受支援||  
|FormatDateTime|不受支援||  
|FormatNumber|不受支援||  
|FormatPercent|不受支援||  
|FreeFile|不受支援||  
|FV|僅限 MDX||  
|GetAllSettings|不受支援||  
|GetAttr|不受支援||  
|GetObject|不受支援||  
|GetSetting|不受支援||  
|Hex|僅限 MDX||  
|Hour|DAX、MDX||  
|Iif|僅限 MDX|**警告**DAX 會使用名稱： IF （logical_test，value_if_true，value_if_false）函數來執行類似的函式。|  
|IMEStatus|不受支援||  
|輸入|不受支援||  
|InputBox|不受支援||  
|InStr|僅限 MDX||  
|InStrRev|不受支援||  
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
|IsObject|不受支援||  
|Join|不受支援||  
|LBound|不受支援||  
|LCase|僅限 MDX||  
|Left|DAX、MDX||  
|Len|DAX、MDX||  
|Loc|不受支援||  
|LOF|不受支援||  
|Log|僅限 MDX|**重要事項**DAX 會使用相同的名稱來執行不同的函式;記錄（數位，基底）函數。 依照給定引數所指定的底數，傳回數字的對數。|  
|LTrim|僅限 MDX||  
|MacID|不受支援||  
|MacScript|不受支援||  
|Mid|DAX、MDX||  
|Minute|DAX、MDX||  
|MIRR|僅限 MDX||  
|Month|DAX、MDX||  
|MonthName|不受支援||  
|MsgBox|不受支援||  
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
|Replace|不受支援||  
|RGB|僅限 MDX||  
|Right|DAX、MDX||  
|Rnd|僅限 MDX||  
|Round|DAX、MDX||  
|RTrim|僅限 MDX||  
|Second|DAX、MDX||  
|Seek|不受支援||  
|Sgn|DAX、MDX||  
|殼層|不受支援||  
|Sin|僅限 MDX||  
|SLN|僅限 MDX||  
|Space|僅限 MDX||  
|Spc|不受支援||  
|Split|不受支援||  
|Sqr|僅限 MDX||  
|Str|僅限 MDX||  
|StrComp|僅限 MDX||  
|StrConv|僅限 MDX||  
|String|僅限 MDX||  
|StrReverse|不受支援||  
|Switch|僅限 MDX||  
|SYD|僅限 MDX||  
|索引標籤|不受支援||  
|Tan|僅限 MDX||  
|時間|不受支援||  
|計時器|僅限 MDX||  
|TimeSerial|僅限 MDX||  
|TimeValue|DAX、MDX||  
|Trim|DAX、MDX||  
|TypeName|僅限 MDX||  
|UBound|不受支援||  
|UCase|僅限 MDX||  
|Val|僅限 MDX||  
|VarType|不受支援||  
|Weekday|DAX、MDX||  
|WeekdayName|不受支援||  
|Year|DAX、MDX||  
  
  
