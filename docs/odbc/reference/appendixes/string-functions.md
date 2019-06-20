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
manager: craigg
ms.openlocfilehash: 948e22d9a4514e4ed7b211398ac28a7338b1c0ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735146"
---
# <a name="string-functions"></a>字串函數
下表列出字串操作函數。 應用程式可以判斷驅動程式支援哪些字串函式藉由呼叫**SQLGetInfo**具有*資訊類型*SQL_STRING_FUNCTIONS。  
  
## <a name="remarks"></a>備註  
 引數可以分成*string_exp*可以是資料行名稱*字元字串常值*，或另一個純量函式，其中表示基礎資料類型，為 SQL_CHAR、 SQL_ 的結果VARCHAR 或 SQL_LONGVARCHAR。  
  
 引數可以分成*character_exp*是可變長度字元字串。  
  
 引數可以分成*開始*，*長度*，或*計數*可以是*數值常值*或結果的另一個純量函式，其中基礎資料類型可以表示為 SQL_TINYINT、 SQL_SMALLINT 或 SQL_INTEGER。  
  
 此處所列的字串函數是以 1 為基礎;也就是說，在字串中的第一個字元是字元 1。  
  
 在 ODBC 3.0，才能符合 SQL-92 收錄 BIT_LENGTH、 CHAR_LENGTH、 CHARACTER_LENGTH、 OCTET_LENGTH，與位置字串純量函式。  
  
|函數|描述|  
|--------------|-----------------|  
|**ASCII(** _string_exp_ **)**  (ODBC 1.0)|傳回的最左邊字元的 ASCII 字碼值*string_exp*做為整數。|  
|**BIT_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|傳回字串運算式的長度 (以位元為單位)。<br /><br /> 不只適用於字串資料類型無法運作，因此將不會隱含地轉換*string_exp*字串而會傳回任何給定的資料類型 （內部） 大小。|  
|**CHAR(** _code_ **)**  (ODBC 1.0)|已將 ASCII 字元程式碼所指定值傳回*程式碼*。 值*程式碼*應該是介於 0 到 255 之間; 否則傳回的值是資料來源而定。|  
|**CHAR_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|以字元為單位的字串運算式，傳回的長度，如果字串運算式的字元資料類型;否則，傳回以位元組為單位的字串運算式 （最小整數不大於或等於除以 8 位元數） 的長度。 （這個函式是 CHARACTER_LENGTH 函式相同）。|  
|**CHARACTER_LENGTH(** _string_exp_ **)**  (ODBC 3.0)|以字元為單位的字串運算式，傳回的長度，如果字串運算式的字元資料類型;否則，傳回以位元組為單位的字串運算式 （最小整數不大於或等於除以 8 位元數） 的長度。 （這個函式是 CHAR_LENGTH 函式相同）。|  
|**CONCAT(** _string_exp1_,_string_exp2_ **)**  (ODBC 1.0)|傳回字元字串的串連結果*string_exp2*要*string_exp1*。 產生的字串為 DBMS 相依。 例如，如果資料行來表示*string_exp1*包含 NULL 值，DB2 會傳回 NULL，但 SQL Server 會傳回非 NULL 字串。|  
|**DIFFERENCE(** _string_exp1_,_string_exp2_ **)**  (ODBC 2.0)|傳回整數值，指出的 SOUNDEX 函式所傳回的值之間的差異*string_exp1*並*string_exp2*。|  
|**INSERT(** _string_exp1_, *start*, *length*, _string_exp2_ **)**  (ODBC 1.0)|傳回字元字串位置*長度*從已刪除的字元*string_exp1*，開始位置在*啟動*，和其中*string_exp2*已插入*string_exp，* 開始*啟動*。|  
|**LCASE(** _string_exp_ **)** (ODBC 1.0)|傳回字串中的相等*string_exp*，所有大寫字元轉換成小寫。|  
|**LEFT(** _string_exp_, _count_ **)** (ODBC 1.0)|傳回最左邊*計數*個字元*string_exp*。|  
|**LENGTH(** _string_exp_ **)** (ODBC 1.0)|傳回的字元數*string_exp，* 排除尾端空白。<br /><br /> **長度**只接受字串。 因此會隱含地轉換*string_exp*字串，並傳回此字串 （不是內部的大小的資料類型） 的長度。|  
|**LOCATE(** _string_exp1_, *string_exp2*[, *start*] **)** (ODBC 1.0)|傳回第一個出現的開始位置*string_exp1*內*string_exp2*。 第一個項目搜尋*string_exp1*中的第一個字元位置的開頭*string_exp2*除非選用的引數，*啟動*，指定。 如果*開始*指定時，使用的值所指示的字元位置開始搜尋*開始*。 在中的第一個字元位置*string_exp2*會以值 1。 如果*string_exp1*內找不到*string_exp2*，會傳回值 0。<br /><br /> 如果應用程式可以呼叫以尋找純量函式*string_exp1*， *string_exp2*，並*啟動*引數，驅動程式會傳回 SQL_FN_STR_LOCATE 時**SQLGetInfo**以呼叫*選項*SQL_STRING_FUNCTIONS。 如果應用程式可以呼叫具有唯一的尋找純量函式*string_exp1*並*string_exp2*引數，驅動程式會傳回 SQL_FN_STR_LOCATE_2 時**SQLGetInfo**以呼叫*選項*SQL_STRING_FUNCTIONS。 支援呼叫尋找函式使用兩個或三個引數傳回 SQL_FN_STR_LOCATE 和 SQL_FN_STR_LOCATE_2 驅動程式。|  
|**LTRIM(** _string_exp_ **)** (ODBC 1.0)|傳回的字元*string_exp*，加上前置空格移除。|  
|**OCTET_LENGTH(** _string_exp_ **)** (ODBC 3.0)|傳回字串運算式的長度 (以位元組為單位)。 結果就是不小於位元數的最小整數除以 8。<br /><br /> 不只適用於字串資料類型無法運作，因此將不會隱含地轉換*string_exp*字串而會傳回任何給定的資料類型 （內部） 大小。|  
|**POSITION(** _character_exp_ **IN** _character_exp_ **)** (ODBC 3.0)|第二個字元運算式中傳回第一個字元運算式的位置。 結果是精確數值與實作定義的有效位數和小數位數 0。|  
|**REPEAT(** _string_exp,_ _count_ **)** (ODBC 1.0)|傳回字元字串所組成*string_exp*重複*計數*時間。|  
|**REPLACE(** _string_exp1_, *string_exp2*, _string_exp3_ **)** (ODBC 1.0)|搜尋*string_exp1*的 foroccurrences *string_exp2*，並取代*string_exp3*。|  
|**RIGHT(** _string_exp_, _count_ **)** (ODBC 1.0)|傳回最右邊*計數*個字元*string_exp*。|  
|**RTRIM(** _string_exp_ **)** (ODBC 1.0)|傳回的字元*string_exp*使用尾端空格移除。|  
|**SOUNDEX(** _string_exp_ **)** (ODBC 2.0)|傳回資料來源相關的字元字串，表示文字中的音效*string_exp*。 例如，SQL Server 會傳回 4 個數字的 SOUNDEX 代碼;Oracle 會傳回每個單字的注音標示表示法。|  
|**SPACE(** _count_ **)** (ODBC 2.0)|傳回字元字串，其中包含*計數*空格。|  
|**子字串 (** _string_exp_，*開始*，長度 **)** (ODBC 1.0)|傳回字元字串，衍生自*string_exp*，在所指定的字元位置起始*開始*for*長度*字元。|  
|**UCASE(** _string_exp_ **)** (ODBC 1.0)|傳回字串中的相等*string_exp*，所有小寫字元轉換成大寫。|
