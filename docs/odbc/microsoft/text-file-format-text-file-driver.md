---
title: 文字檔案格式 （文字檔驅動程式） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd2bc95e6fe5468e88fc61dd8ed4adcd985ec052
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633013"
---
# <a name="text-file-format-text-file-driver"></a>文字檔格式 (文字檔驅動程式)
ODBC 文字驅動程式支援這兩個分隔和固定寬度文字檔案。 文字檔案是由選擇性標頭行，零或多個文字行所組成。  
  
 雖然標頭行使用相同的格式為文字檔案中的其他行，但是 ODBC 文字驅動程式會將標頭列項目解譯為資料行名稱，而非資料。  
  
 分隔的文字行包含一或多個資料值，並以分隔符號分隔： 逗號、 定位點或自訂的分隔符號。 整個檔案，就必須使用相同的分隔符號。 Null 資料值會由它們之間沒有資料的資料列中的兩個分隔符號來表示。 分隔的文字行中的字元字串可以用雙引號括住 ("")。 之前或之後分隔的值，可能會不發生任何空格。  
  
 結構描述中指定固定寬度文字行中的每個資料項目的寬度。 Null 資料值會表示以空格。  
  
 資料表是限制為 255 個欄位的最大值。 欄位名稱限制為 64 個字元，且欄位寬度都受限於 32,766 個字元。 記錄僅限於 65,000 個位元組。  
  
 僅適用於單一使用者可以開啟文字檔案。 不支援多個使用者。  
  
 下列文法中，撰寫適用於程式設計人員，會定義 ODBC 文字驅動程式可以讀取文字檔案的格式：  
  
|格式|表示法|  
|------------|--------------------|  
|非斜體|必須輸入所顯示的字元|  
|*italics*|在文法中其他地方定義的引數|  
|brackets ([])|選擇性項目|  
|大括號 ({})|互斥的選項清單|  
|分隔號 (&#124;)|不同的是互斥的選項|  
|省略符號 （...）|可以重複一次以上的項目|  
  
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
>  Schema.ini 檔中指定的固定寬度文字檔案中的每個資料行寬度。  
  
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
>  分隔檔案中，null 值被不以兩個分隔符號之間的任何資料。  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  固定寬度檔案的 null 值被以空格。
