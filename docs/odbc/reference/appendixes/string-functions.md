---
title: 字串函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd4ec3e05acfd4faaafd38a79e48c67d03d86bd4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070167"
---
# <a name="string-functions"></a>字串函式
下表列出字串操作函數。 應用程式可以藉由使用 SQL_STRING_FUNCTIONS 的*資訊類型*來呼叫**SQLGetInfo** ，以判斷驅動程式支援哪些字串函數。  
  
## <a name="remarks"></a>備註  
 表示為*string_exp*的引數可以是資料行的名稱、*字元字串常*值或另一個純量函數的結果，其中基礎資料類型可以表示為 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR。  
  
 表示為*character_exp*的引數是可變長度的字元字串。  
  
 表示為*開始*、*長度*或*計數*的引數可以是*數值常*值或另一個純量函數的結果，其中基礎資料類型可以表示為 SQL_TINYINT、SQL_SMALLINT 或 SQL_INTEGER。  
  
 此處所列的字串函數是以1為基礎;也就是字串中的第一個字元是字元1。  
  
 ODBC 3.0 中已加入 BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH 和位置字串純量函數，以配合 SQL-92。  
  
|函式|描述|  
|--------------|-----------------|  
|**ASCII （** _string_exp_ **）** （ODBC 1.0）|以整數形式傳回*string_exp*最左邊字元的 ASCII 碼值。|  
|**BIT_LENGTH （** _string_exp_ **）** （ODBC 3.0）|傳回字串運算式的長度 (以位元為單位)。<br /><br /> 不適用於字串資料類型，因此不會將*string_exp*隱含地轉換成字串，而是會傳回所提供之任何資料類型的（內部）大小。|  
|**CHAR （** _code_ **）** （ODBC 1.0）|傳回具有程式*代碼*所指定之 ASCII 碼值的字元。 程式*代碼*的值應介於0到255之間;否則，傳回值會相依于資料來源。|  
|**CHAR_LENGTH （** _string_exp_ **）** （ODBC 3.0）|如果字串運算式是字元資料類型，則傳回字串運算式的長度（以字元為單位）;否則，會傳回字串運算式的長度（以位元組為單位）（不小於位數除以8的最小整數）。 （此函式與 CHARACTER_LENGTH 函式相同）。|  
|**CHARACTER_LENGTH （** _string_exp_ **）** （ODBC 3.0）|如果字串運算式是字元資料類型，則傳回字串運算式的長度（以字元為單位）;否則，會傳回字串運算式的長度（以位元組為單位）（不小於位數除以8的最小整數）。 （此函式與 CHAR_LENGTH 函式相同）。|  
|**CONCAT （** _string_exp1_，_string_exp2_**）** （ODBC 1.0）|傳回字元字串，這是將*string_exp2*串連至*string_exp1*的結果。 產生的字串為 DBMS 相依。 例如，如果*string_exp1*所代表的資料行包含 null 值，則 DB2 會傳回 null，但 SQL Server 會傳回非 null 的字串。|  
|**差異（** _string_exp1_、_string_exp2_**）** （ODBC 2.0）|傳回整數值，指出*string_exp1*和*string_exp2*的 SOUNDEX 函數所傳回的值之間的差異。|  
|**INSERT （** _string_exp1_、 *start*、 *length*、 _string_exp2_**）** （ODBC 1.0）|傳回字元字串，其中的*長度*字元已從*string_exp1*中刪除，從*開始*，到*string_exp2*插入*string_exp，* 從*開始*。|  
|**LCASE （** _string_exp_ **）** （ODBC 1.0）|傳回*string_exp*中的字串，並將所有大寫字元轉換成小寫。|  
|**LEFT （** _string_exp_， _count_**）** （ODBC 1.0）|傳回*string_exp*的最左邊*計數*字元。|  
|**長度（** _string_exp_ **）** （ODBC 1.0）|傳回 string_exp 中的字元數 *，* 不包括尾端空白。<br /><br /> **長度**只接受字串。 因此，會將*string_exp*隱含地轉換為字串，並傳回這個字串的長度（而不是資料類型的內部大小）。|  
|**找出（** _string_exp1_， *string_exp2*[， *start*]**）** （ODBC 1.0）|傳回*string_exp2*內第一次出現*string_exp1*的開始位置。 搜尋第一次出現的*string_exp1*從*string_exp2*中的第一個字元位置開始，除非指定了選擇性的引數*start*。 如果指定*start* ，則搜尋會以*start*的值所指示的字元位置開始。 *String_exp2*中的第一個字元位置是以值1來表示。 如果在*string_exp2*內找不到*string_exp1* ，則會傳回0值。<br /><br /> 如果應用程式可以使用*string_exp1*、 *string_exp2*和*START*引數來呼叫尋找純量函數，驅動程式會在呼叫**SQLGetInfo**時，使用 SQL_STRING_FUNCTIONS 的*選項*來傳回 SQL_FN_STR_LOCATE。 如果應用程式可以呼叫僅具有*string_exp1*和*string_exp2*引數的尋找純量函數，則當使用 SQL_STRING_FUNCTIONS 的*選項*來呼叫**SQLGetInfo**時，驅動程式會傳回 SQL_FN_STR_LOCATE_2。 支援使用兩個或三個引數呼叫尋找函數的驅動程式會同時傳回 SQL_FN_STR_LOCATE 和 SQL_FN_STR_LOCATE_2。|  
|**LTRIM （** _string_exp_ **）** （ODBC 1.0）|傳回已移除開頭空白的*string_exp*字元。|  
|**OCTET_LENGTH （** _string_exp_ **）** （ODBC 3.0）|傳回字串運算式的長度 (以位元組為單位)。 結果就是不小於位元數的最小整數除以 8。<br /><br /> 不適用於字串資料類型，因此不會將*string_exp*隱含地轉換成字串，而是會傳回所提供之任何資料類型的（內部）大小。|  
|**POSITION （** __ **在** _character_exp_中 character_exp **）** （ODBC 3.0）|傳回第二個字元運算式中第一個字元運算式的位置。 結果會是具有執行定義的有效位數和小數位數為0的精確數值。|  
|**重複（** _string_exp、_ _計數_**）** （ODBC 1.0）|傳回由*string_exp*重複*計數*次所組成的字元字串。|  
|**REPLACE （** _string_exp1_， *string_exp2*， _string_exp3_**）** （ODBC 1.0）|搜尋*string_exp2*的*string_exp1* foroccurrences，並以*string_exp3*取代。|  
|**RIGHT （** _string_exp_， _count_**）** （ODBC 1.0）|傳回*string_exp*的最右邊*計數*字元。|  
|**RTRIM （** _string_exp_ **）** （ODBC 1.0）|傳回已移除尾端空白之*string_exp*的字元。|  
|**SOUNDEX （** _string_exp_ **）** （ODBC 2.0）|傳回資料來源相依的字元字串，代表*string_exp*中的單字音效。 例如，SQL Server 會傳回4位數的 SOUNDEX 代碼;Oracle 會傳回每個單字的語音標記法。|  
|**空間（** _計數_ **）** （ODBC 2.0）|傳回由*計數*空格組成的字元字串。|  
|**SUBSTRING （** _string_exp_、 *start*、length **）** （ODBC 1.0）|傳回衍生自*string_exp*的字元字串，從*開始**長度*字元所指定的字元位置開始。|  
|**UCASE （** _string_exp_ **）** （ODBC 1.0）|傳回等於*string_exp*中的字串，其中所有小寫字元都轉換為大寫。|
