---
title: 文字檔案格式 （文字檔案驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2f0de1d7b5ca14c5ae51cd057244d0c3252780a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="text-file-format-text-file-driver"></a>文字檔案格式 （文字檔案驅動程式）
ODBC 文字驅動程式支援分隔和固定寬度文字檔。 文字檔案是由選擇性標頭行，零或多個文字行所組成。  
  
 標頭行做為文字檔案中的其他程式使用相同的格式，雖然文字 ODBC 驅動程式會解譯資料行名稱，而不是資料的標頭列項目。  
  
 分隔的文字行包含以分隔符號隔開的一個或多個資料值： 逗號、 索引標籤上或自訂的分隔符號。 整個檔案必須使用相同的分隔符號。 它們之間沒有資料的資料列中的兩個分隔符號以代表 null 資料值。 字元字串中分隔的文字行可以括在雙引號 ("")。 分隔值的前後，可能會發生沒有空白。  
  
 結構描述中指定固定寬度的文字行中的每個資料項目的寬度。 以空白代表 null 資料值。  
  
 資料表會限制為 255 個欄位的最大值。 欄位名稱限制為 64 個字元，且欄位寬度都限制為可有 32,766 個字元。 記錄的上限為 65000 個位元組。  
  
 只能為單一使用者可以開啟文字檔。 不支援多個使用者。  
  
 下列文法中，撰寫的程式設計人員定義 ODBC 文字驅動程式可以讀取的文字檔案的格式：  
  
|格式|表示法|  
|------------|--------------------|  
|非斜體|必須依照顯示輸入的字元|  
|*斜體*|在文法中其他地方定義的引數|  
|括號 ([])|選擇性項目|  
|大括號 ({})|互斥的選項清單|  
|分隔號 (&#124;)|個別互斥的選項|  
|省略符號 （...）|可以重複一次以上的項目|  
  
 將文字檔的格式如下：  
  
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
>  Schema.ini 檔中指定固定寬度的文字檔中每個資料行的寬度。  
  
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
>  Schema.ini 檔中指定自訂分隔的文字檔案中的分隔符號。  
  
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
>  若是分隔的檔案，null 值會不以兩個分隔符號之間的任何資料。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  若是固定寬度的檔案，空格會以 null 值。
