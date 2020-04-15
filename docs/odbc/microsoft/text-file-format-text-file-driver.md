---
title: 文字檔案格式 (文字檔案驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303089"
---
# <a name="text-file-format-text-file-driver"></a>文字檔格式 (文字檔驅動程式)
ODBC 文字驅動程式支援分隔和固定寬度文本檔。 文字檔由可選的頁眉行和零行或更多文本行組成。  
  
 儘管標題行使用與文本檔中其他行相同的格式,但 ODBC 文本驅動程式將標題行條目解釋為列名稱,而不是數據。  
  
 分隔文字行包含一個或多個由分隔符分隔的數據值:逗號、選項卡或自定義分隔符。 在整個文件中必須使用相同的分隔符。 空資料值由行中的兩個分隔符表示,它們之間沒有數據。 分隔文字列中的字串可以用雙引號 ("")括起來。 在分隔值之前或之後,不能出現空白。  
  
 在架構中指定了固定寬度文本行中每個數據條目的寬度。 空數據值表示為空白。  
  
 表最多只能限制 255 個字段。 欄位名稱限制為 64 個字元,欄位寬度限制為 32,766 個字元。 記錄限制為 65,000 位元組。  
  
 文字檔只能為單個用戶打開。 不支援多個使用者。  
  
 以下文法是為程式師編寫的,它定義了 ODBC 文字驅動程式可以讀取的文字檔的格式:  
  
|[格式]|表示法|  
|------------|--------------------|  
|非斜體|必須輸入的字元(如圖所示)|  
|*斜體 字*|語法中其他位置定義的參數|  
|括弧 (*)|選擇性項目|  
|大括號{}( )|互斥選項清單|  
|垂直條 (&#124;)|單獨的互斥選擇|  
|省略符號 (...)|可以重複一次或多次的項目|  
  
 文字檔案格式為:  
  
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
>  固定寬度文字檔中每列的寬度在 Schema.ini 檔中指定。  
  
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
>  自訂分隔文字檔中的分隔符在 Schema.ini 檔中指定。  
  
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
>  對於分隔檔,NULL 由兩個分隔符之間沒有資料表示。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  對於固定寬度檔,NULL 由空格表示。
