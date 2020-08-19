---
description: 間隔常值
title: 間隔常值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd065091127645a45b836781fc6edf6c701e6685
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425030"
---
# <a name="interval-literals"></a>間隔常值
ODBC 要求所有驅動程式都必須支援將 SQL_CHAR 或 SQL_VARCHAR 資料類型轉換為所有 C 間隔資料類型。 但是，如果基礎資料來源不支援間隔資料類型，則驅動程式必須知道 SQL_CHAR 欄位中值的正確格式，才能支援這些轉換。 同樣地，ODBC 要求任何 ODBC C 型別可轉換成 SQL_CHAR 或 SQL_VARCHAR，因此驅動程式必須知道字元欄位中所儲存之間隔的格式。 本章節描述間隔常值的語法，驅動程式寫入器需要使用此語法，在轉換期間驗證 SQL_CHAR 欄位，或從 C 間隔資料類型進行轉換。  
  
> [!NOTE]  
>  間隔常值的完整 BNF 語法顯示于附錄 C： SQL 文法中的區段 [間隔常值語法](../../../odbc/reference/appendixes/interval-literal-syntax.md) 。  
  
 若要將間隔常值傳遞為 SQL 語句的一部分，請針對間隔常值定義一個 escape 子句語法。 如需詳細資訊，請參閱 [日期、時間和時間戳記常](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)值。  
  
 間隔常值的格式如下：  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 其中「間隔」表示字元常值為間隔。 正負號可以是加號或減號;它是在間隔字串之外，而且是選擇性的。  
  
 間隔限定詞可以是單一 datetime 欄位，也可以由兩個 datetime 欄位組成，格式 \<*leading field*> 為： TO \<*trailing field*> 。  
  
-   當間隔是由單一欄位所組成時，單一欄位可以是非第二個欄位，而且可能會在括弧中伴隨選擇性的前置精確度。 單一 datetime 欄位也可以是第二個欄位，此欄位可能伴隨著選擇性的前置精確度、選擇性的小數秒有效位數（以括弧括住），或兩者都有。 如果秒欄位有前置精確度和小數秒有效位數，則會以逗號分隔。 如果 seconds 欄位具有小數秒精確度，它也必須有前置精確度。  
  
-   當間隔是由開頭和尾端欄位所組成時，前置欄位會是一個非第二個欄位，可能會伴隨以括弧括住的間隔前置欄位精確度。 尾端欄位可以是非第二個欄位，也可以是第二個欄位，可能伴隨著以括弧括住的間隔小數秒有效位數。  
  
 *值*的間隔字串以單引號括住。 它可以是年中的常值或日期時間常值。 *值*中字串的格式取決於下列規則：  
  
-   字串包含所隱含之每個欄位的十進位值 \<*interval* *qualifier*> 。  
  
-   如果間隔精確度包含 YEAR 和 MONTH 欄位，這些欄位的值就會以減號隔開。  
  
-   如果間隔精確度包含欄位 DAY 和小時，這些欄位的值會以空格分隔。  
  
-   如果間隔精確度包含欄位小時，而較低順序欄位 (分鐘和秒) ，則這些欄位的值會以冒號分隔。  
  
-   如果間隔精確度包含第二個欄位，且表示或隱含的秒數有效位數為非零值，則在第二個小數部分的第一個數位之前，緊接在第二個數字之前的字元是句號。  
  
-   沒有任何欄位可以有兩位數以上的長度，但：  
  
    -   前置欄位的值可以是所表達或默示的間隔前置精確度的完整值。  
  
    -   第二個欄位的小數部分可以是表示或隱含的秒數有效位數。  
  
    -   尾端欄位遵循西曆的一般條件約束。  (查看 [西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。 )   
  
 下表依間隔列出 ODBC escape 子句中包含的有效間隔常值範例。 Escape 子句的語法如下所示：  
  
> [!NOTE]  
>  *{間隔符號間隔-字串間隔-辨識符號}*  
  
|常值 escape 子句|指定的間隔|  
|---------------------------|------------------------|  
|{INTERVAL ' 326 ' 年 (4) }|指定326年的間隔。 間隔前置精確度為4。|  
|{INTERVAL ' 326 ' MONTH (3) }|指定326個月的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 3261 ' DAY (4) }|指定3261天的間隔。 間隔前置精確度為4。|  
|{INTERVAL ' 163 ' 小時 (3) }|指定163天的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 163 ' 分鐘 (3) }|指定163分鐘的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 223.16 ' 第二 (3，2) }|指定223.16 秒的間隔。 間隔前置精確度為3，而秒有效位數為2。|  
|{INTERVAL ' 163-11 ' 年 (3) 至月}|指定163年和11個月的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 163 12 ' DAY (3) 到 HOUR}|指定163天和12小時的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 163 12:39 ' DAY (3) 至 MINUTE}|指定163天、12小時和39分鐘的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 163 12：39： 59.163 ' DAY (3) 第二 (3) }|指定163天、12小時、39分鐘和59.163 秒的間隔。 間隔前置精確度為3，而秒有效位數為3。|  
|{INTERVAL ' 163:39 ' 小時 (3) 到分鐘}|指定163小時和39分鐘的間隔。 間隔前置精確度為3。|  
|{INTERVAL ' 163：39： 59.163 ' 小時 (3) 至第二 (4) }|指定163小時、39分鐘和59.163 秒的間隔。 間隔前置精確度為3，而秒有效位數為4。|  
|{INTERVAL ' 163： 59.163 ' 分鐘 (3) 至第二 (5) }|指定163分鐘和59.163 秒的間隔。 間隔前置精確度為3，而秒有效位數為5。|  
|{INTERVAL-' 16 23：39： 56.23 ' 日到秒}|指定減去16天、23小時、39分鐘和56.23 秒的間隔。 隱含的前置精確度為2，而隱含的秒數有效位數為6。|  
  
 下表列出無效間隔常值的範例：  
  
|常值 escape 子句|不正確原因|  
|---------------------------|------------------------|  
|{INTERVAL ' 163 ' 小時 (2) }|間隔前置精確度為2，但前置欄位的值為163。|  
|{INTERVAL ' 223.16 ' 第二 (2，2) }<br /><br /> {INTERVAL ' 223.16 ' 第二 (3，1) }|在第一個範例中，前置精確度太小，而第二個範例中的秒數有效位數太小。|  
|{INTERVAL ' 223.16 ' 秒}<br /><br /> {INTERVAL ' 223 ' 年}|因為未指定前置精確度，所以會預設為2，而該值太小而無法容納指定的常值。|  
|{INTERVAL ' 22.1234567 ' 秒}|未指定秒數有效位數，因此預設為6。 常值在小數點後面有七位數。|  
|{INTERVAL ' 163-13 ' 年 (3) 至月}<br /><br /> {INTERVAL ' 163 65 ' DAY (3) 到 HOUR}<br /><br /> {INTERVAL ' 163 62:39 ' DAY (3) 至 MINUTE}<br /><br /> {INTERVAL ' 163 12：125： 59.163 ' DAY (3) 第二 (3) }<br /><br /> {INTERVAL ' 163:144 ' 小時 (3) 到分鐘}<br /><br /> {INTERVAL ' 163：567： 234.163 ' 小時 (3) 至第二 (4) }<br /><br /> {INTERVAL ' 163： 591.163 ' 分鐘 (3) 至第二 (5) }|尾端欄位未遵循西曆的規則。|
