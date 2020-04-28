---
title: 文本檔案格式（文字檔驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801433e0180bb07cb2d09a59db2bb74be012cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303089"
---
# <a name="text-file-format-text-file-driver"></a>文字檔格式 (文字檔驅動程式)
ODBC 文字驅動程式同時支援分隔和固定寬度的文字檔。 文字檔是由選擇性的標頭行和零或多個文字行所組成。  
  
 雖然標頭行使用與文字檔中其他行相同的格式，但 ODBC 文字驅動程式會將標頭行專案解讀為數據行名稱，而不是資料。  
  
 分隔的文字行包含一或多個以分隔符號分隔的資料值：逗號、定位字元或自訂分隔符號。 整個檔案中都必須使用相同的分隔符號。 Null 資料值在資料列中以兩個分隔符號表示，其中沒有任何資料。 分隔文字行中的字元字串可以用雙引號（""）括住。 分隔值前後不能出現空白。  
  
 固定寬度文字行中每個資料項目的寬度都是在架構中指定。 Null 資料值會以空白表示。  
  
 資料表限制為最多255個欄位。 功能變數名稱限制為64個字元，而欄位寬度限制為32766個字元。 記錄限制為65000個位元組。  
  
 只有單一使用者可以開啟文字檔。 不支援多個使用者。  
  
 下列針對程式設計人員所撰寫的文法，會定義可由 ODBC 文字驅動程式讀取的文本檔案格式：  
  
|[格式]|表示法|  
|------------|--------------------|  
|非斜體|必須如所示輸入的字元|  
|*斜體*|在文法中的其他位置定義的引數|  
|方括弧（[]）|選擇性項目|  
|大括弧{}（）|互斥選項的清單|  
|分隔號（&#124;）|個別互斥選項|  
|省略符號 (...)|可以重複一次或多次的專案|  
  
 文字檔的格式為：  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  固定寬度文字檔中每個資料行的寬度都是在 schema.ini 檔案中指定。  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  在以自訂分隔的文字檔中的分隔符號是在 schema.ini 檔案中指定。  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  針對分隔的檔案，Null 是以兩個分隔符號之間沒有資料來表示。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  針對固定寬度的檔案，Null 會以空格表示。
