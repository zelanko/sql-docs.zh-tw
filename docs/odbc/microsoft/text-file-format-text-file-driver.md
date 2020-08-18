---
description: 文字檔格式 (文字檔驅動程式)
title: 文本檔案格式 (文字檔驅動程式) |Microsoft Docs
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
ms.openlocfilehash: fb402f0f186529da33974b77ffeecdd7ed788d53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449090"
---
# <a name="text-file-format-text-file-driver"></a>文字檔格式 (文字檔驅動程式)
ODBC 文字驅動程式支援分隔和固定寬度的文字檔。 文字檔包含選擇性的標頭行和零或多個文字行。  
  
 雖然標頭行會使用與文字檔中其他行相同的格式，但是 ODBC 文字驅動程式會將標頭明細專案解釋為數據行名稱，而不是資料。  
  
 分隔的文字行包含一或多個以分隔符號分隔的資料值：逗號、定位字元或自訂分隔符號。 整個檔案都必須使用相同的分隔符號。 Null 資料值會在資料列中以兩個不含資料的分隔符號表示。 分隔文字行中的字元字串可以用雙引號括住 ( "" ) 。 分隔值之前或之後都不能出現任何空白。  
  
 在架構中指定固定寬度文字行中每個資料項目目的寬度。 Null 資料值會以空白表示。  
  
 資料表最多隻能有255個欄位。 功能變數名稱限制為64個字元，欄位寬度限制為32766個字元。 記錄的限制為65000個位元組。  
  
 只有單一使用者可以開啟文字檔。 不支援多個使用者。  
  
 下列為程式設計人員撰寫的文法定義了 ODBC 文字驅動程式可讀取的文本檔案格式：  
  
|格式|表示法|  
|------------|--------------------|  
|非斜體|必須輸入的字元（如下所示）|  
|*斜 體 字*|在文法中的其他位置定義的引數|  
|括弧 ( [] ) |選擇性項目|  
|括弧 ({}) |互斥選擇的清單|  
|垂直線 ( # A0) |個別的互斥選擇|  
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
>  在 Schema.ini 檔案中，會指定固定寬度文字檔中每個資料行的寬度。  
  
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
>  在 Schema.ini 檔案中指定自訂分隔文字檔中的分隔符號。  
  
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
>  若為分隔的檔案，在兩個分隔符號之間不會有任何資料代表 Null。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  若為固定寬度的檔案，則會以空格表示 Null。
