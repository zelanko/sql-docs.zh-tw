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
manager: kfile
ms.openlocfilehash: 327a801ce725987d68236efcfddbf8a4e7231ea9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251553"
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函數


  本文件包含中可用的所有 VBA 函數的交互的參考[Visual Basic for Applications 函式](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications)MDX 支援; 此外，此清單包含附註與 DAX 語言的功能是否相等時.  
  
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
|命令|不支援||  
|Cos|僅限 MDX||  
|CreateObject|不支援||  
|CSng|僅限 MDX||  
|CStr|僅限 MDX||  
|CurDir|不支援||  
|CVar|僅限 MDX||  
|CVErr|不支援||  
|Date|僅限 MDX|**警告**DAX 會實作不同的函式具有相同名稱，用來從指定的引數產生日期類型值的 DATE (Year，Month，Day) 函數|  
|DateAdd|僅限 MDX|**警告**DAX 會實作不同的函式具有相同名稱： dateadd (\<日期 >，< number_of_intervals >，\<間隔 >) 函數，用來移位給定的日期，由數項給定的間隔|  
|DateDiff]|僅限 MDX||  
|DatePart|僅限 MDX||  
|DateSerial|僅限 MDX||  
|DateValue]|DAX、MDX||  
|Day|DAX、MDX||  
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
|篩選|不支援|**警告**MDX 會實作具有相同名稱的不同函式; FILTER （Set_Expression，Logical_Expression） 函數傳回的結果篩選指定的集合，根據給定的引數的搜尋條件的集合<br /><br /> **警告**DAX 會實作不同的函式具有相同名稱; 篩選器 (\<資料表 >，\<篩選 >) 函數會傳回代表另一個資料表或從指定的引數的運算式的子集的資料表|  
|Fix|僅限 MDX||  
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
|Hour|DAX、MDX||  
|Iif|僅限 MDX|**警告**DAX 會實作類似的函式名稱：IF (logical_test，value_if_true，value_if_false) 函數。|  
|IMEStatus|不支援||  
|輸入|不支援||  
|InputBox|不支援||  
|InStr|僅限 MDX||  
|InStrRev|不支援||  
|int|DAX、MDX||  
|IPmt|僅限 MDX||  
|IRR|僅限 MDX||  
|IsArray|僅限 MDX||  
|只有 IsDateMDX||  
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
|Log|僅限 MDX|**重要**DAX 會實作不同的函式具有相同名稱，LOG (number，base) 函數。 依照給定引數所指定的底數，傳回數字的對數。|  
|LTrim|僅限 MDX||  
|MacID|不支援||  
|MacScript|不支援||  
|Mid|DAX、MDX||  
|Minute|DAX、MDX||  
|MIRR|僅限 MDX||  
|Month|DAX、MDX||  
|MonthName|不支援||  
|MsgBox|不支援||  
|現在|DAX、MDX||  
|NPer]|僅限 MDX||  
|NPV|僅限 MDX||  
|Oct|僅限 MDX||  
|資料分割|僅限 MDX||  
|Pmt|僅限 MDX||  
|PPmt|僅限 MDX||  
|PV|僅限 MDX||  
|QBColor|僅限 MDX||  
|Rate|僅限 MDX||  
|取代|不支援||  
|RGB|僅限 MDX||  
|Right|DAX、MDX||  
|Rnd|僅限 MDX||  
|捨入|DAX、MDX||  
|RTrim|僅限 MDX||  
|第二個|DAX、MDX||  
|Seek|不支援||  
|Sgn|DAX、MDX||  
|Shell|不支援||  
|Sin|僅限 MDX||  
|SLN|僅限 MDX||  
|Space|僅限 MDX||  
|Spc|不支援||  
|「分岔」|不支援||  
|Sqr|僅限 MDX||  
|Str|僅限 MDX||  
|StrComp|僅限 MDX||  
|StrConv|僅限 MDX||  
|String]|僅限 MDX||  
|StrReverse|不支援||  
|參數|僅限 MDX||  
|SYD|僅限 MDX||  
|索引標籤|不支援||  
|Tan|僅限 MDX||  
|Time|不支援||  
|Timer|僅限 MDX||  
|TimeSerial|僅限 MDX||  
|TimeValue|DAX、MDX||  
|修剪]|DAX、MDX||  
|TypeName|僅限 MDX||  
|UBound|不支援||  
|UCase|僅限 MDX||  
|Val|僅限 MDX||  
|VarType|不支援||  
|Weekday|DAX、MDX||  
|WeekdayName|不支援||  
|Year|DAX、MDX||  
  
  
