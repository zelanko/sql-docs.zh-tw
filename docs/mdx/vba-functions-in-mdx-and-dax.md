---
title: MDX 和 DAX 中的 VBA 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 420452fd-9507-4093-8857-71d3e70d96cc
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5f8b50aaef88b4bfd17cace3877da88e6939605e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="vba-functions-in-mdx-and-dax"></a>MDX 和 DAX 中的 VBA 函數
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  本文件包含之所有 VBA 函數中可用的交互的參考[應用程式函式的 Visual Basic](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) MDX 支援; 此外，此清單包含附註和 DAX 語言的功能等價時.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Visual Basic for Applications 函數參考  
  
|函數名稱|Supported|注意|  
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
|日期|僅限 MDX|**警告**DAX 會實作具有相同的不同函式名稱，用來從指定的引數產生日期類型值的 DATE (Year，Month，Day) 函數|  
|DateAdd|僅限 MDX|**警告**DAX 會實作具有相同的不同函式名稱，則 DATEADD (\<日期 >，< number_of_intervals >，\<間隔 >) 函數，用來移位給定的日期，由數項給定的間隔|  
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
|篩選|不支援|**警告**MDX 會實作具有相同名稱的不同函式; FILTER （Set_Expression，Logical_Expression） 函數會傳回所產生篩選根據搜尋條件，從指定的引數的指定的集合的集合<br /><br /> **警告**DAX 會實作具有相同的不同函式名稱： FILTER (\<資料表 >，\<篩選 >) 函數會傳回代表另一個資料表或從指定的引數運算式的子集的資料表|  
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
|Iif|僅限 MDX|**警告**DAX 會實作名稱類似的函式： IF (logical_test，value_if_true，value_if_false) 函數。|  
|IMEStatus|不支援||  
|Input|不支援||  
|InputBox|不支援||  
|InStr|僅限 MDX||  
|InStrRev|不支援||  
|整數|DAX、MDX||  
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
|Log|僅限 MDX|**重要**DAX 會實作具有相同的不同函式名稱，LOG (數字，base) 函數。 依照給定引數所指定的底數，傳回數字的對數。|  
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
  
  
