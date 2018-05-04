---
title: 字串函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a38b4c3ce271661373fb7b809fdf8c80e7ff19ec
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="string-functions"></a>字串函數
下表列出字串操作函數。 應用程式就可以判斷驅動程式支援的字串函式呼叫**SQLGetInfo**與*資訊類型*SQL_STRING_FUNCTIONS。  
  
## <a name="remarks"></a>備註  
 引數表示為*string_exp*可以是資料行名稱*字元字串常值*，或另一個純量函數，其中基礎資料類型可以表示成 SQL_CHAR，SQL_ 結果VARCHAR 或 SQL_LONGVARCHAR。  
  
 引數表示為*character_exp*可變長度的字元字串。  
  
 引數表示為*啟動*，*長度*，或*計數*可以*數值常值*或另一個純量函數的結果，基礎資料類型可以表示為 SQL_TINYINT、 SQL_SMALLINT 或 SQL_INTEGER。  
  
 此處所列的字串函數是以 1 為基礎;也就是說，在字串中的第一個字元是字元 1。  
  
 在 ODBC 3.0 以配合 SQL 92 已加入 BIT_LENGTH、 CHAR_LENGTH、 CHARACTER_LENGTH、 OCTET_LENGTH，與位置字串純量函數。  
  
|函數|Description|  
|--------------|-----------------|  
|**ASCII (** *string_exp* **)** (ODBC 1.0)|傳回的最左邊字元的 ASCII 字碼值*string_exp*為整數。|  
|**BIT_LENGTH (** *string_exp* **)** (ODBC 3.0)|傳回字串運算式的長度 (以位元為單位)。<br /><br /> 並不只適用於字串資料類型，因此將不會隱含地轉換*string_exp*字串而會傳回任何給定的資料類型 （內部） 大小。|  
|**CHAR (** *程式碼* **)** (ODBC 1.0)|已將 ASCII 字元的程式碼所指定的值傳回*程式碼*。 值*程式碼*應該介於 0 和 255 之間; 否則傳回的值就是資料來源而定。|  
|**CHAR_LENGTH (** *string_exp* **)** (ODBC 3.0)|傳回以字元為單位的字串運算式的長度的字串運算式的字元資料類型; 如果否則，傳回的長度，以位元組為單位的字串運算式 （的最小整數不大於或等於除以 8 位元數目）。 （這個函式是 CHARACTER_LENGTH 函式一樣）。|  
|**CHARACTER_LENGTH (** *string_exp* **)** (ODBC 3.0)|傳回以字元為單位的字串運算式的長度的字串運算式的字元資料類型; 如果否則，傳回的長度，以位元組為單位的字串運算式 （的最小整數不大於或等於除以 8 位元數目）。 （這個函式是 CHAR_LENGTH 函式一樣）。|  
|**CONCAT (** *string_exp1*，*string_exp2 * * *)** (ODBC 1.0)|傳回字元字串的串連結果*string_exp2*至*string_exp1*。 產生的字串為 DBMS 相依。 例如，如果資料行來表示*string_exp1*包含 NULL 值，DB2 會傳回 NULL，但 SQL Server 會傳回非 NULL 字串。|  
|**差異 (** *string_exp1*，*string_exp2 * * *)** (ODBC 2.0)|傳回整數值，指出的 SOUNDEX 函式所傳回的值之間的差異*string_exp1*和*string_exp2*。|  
|**插入 (** *string_exp1*，*啟動*，*長度*， *string_exp2 * * *)** (ODBC 1.0)|傳回字元字串位置*長度*字元已從*string_exp1*開始在*啟動*，及在何處*string_exp2*已插入至*string_exp，*開始*啟動*。|  
|**LCASE (** *string_exp* **)** (ODBC 1.0)|傳回字串中的相等*string_exp*，所有大寫字元轉換成小寫。|  
|**LEFT (** *string_exp*，*計數 * * *)** (ODBC 1.0)|傳回最左邊*計數*字元*string_exp*。|  
|**長度 (** *string_exp* **)** (ODBC 1.0)|傳回的字元數*string_exp，*但不包括尾端空白。<br /><br /> **長度**只接受字串。 因此會隱含地轉換*string_exp*為字串，並傳回此字串 （不內部大小的資料類型） 的長度。|  
|**找出 (** *string_exp1*， *string_exp2*[，*啟動*]**)** (ODBC 1.0)|傳回第一個出現的開始位置*string_exp1*內*string_exp2*。 第一個出現的搜尋*string_exp1*開頭中的第一個字元位置*string_exp2*除非選用的引數，*啟動*，指定。 如果*啟動*指定，則使用的值所指定的字元位置開始搜尋*啟動*。 第一個字元放在*string_exp2*係以值 1。 如果*string_exp1*內找不到*string_exp2*，會傳回值 0。<br /><br /> 如果應用程式可以呼叫尋找純量函數， *string_exp1*， *string_exp2*，和*啟動*引數，驅動程式會傳回 SQL_FN_STR_LOCATE 時**SQLGetInfo**呼叫*選項*SQL_STRING_FUNCTIONS。 如果應用程式可以呼叫尋找純量函數中的，只有*string_exp1*和*string_exp2*引數，驅動程式會傳回 SQL_FN_STR_LOCATE_2 時**SQLGetInfo**呼叫*選項*SQL_STRING_FUNCTIONS。 支援呼叫尋找函式使用兩個或三個引數傳回 SQL_FN_STR_LOCATE 和 SQL_FN_STR_LOCATE_2 驅動程式。|  
|**LTRIM (** *string_exp* **)** (ODBC 1.0)|傳回的字元*string_exp*，加上前置空格移除。|  
|**OCTET_LENGTH (** *string_exp* **)** (ODBC 3.0)|傳回字串運算式的長度 (以位元組為單位)。 結果就是不小於位元數的最小整數除以 8。<br /><br /> 並不只適用於字串資料類型，因此將不會隱含地轉換*string_exp*字串而會傳回任何給定的資料類型 （內部） 大小。|  
|**位置 (** *character_exp* **IN** *character_exp * * *)** (ODBC 3.0)|第二個字元運算式中傳回第一個字元運算式的位置。 結果是精確數值實作所定義的有效位數與小數位數為 0。|  
|**重複 (** *string_exp，* *計數 * * *)** (ODBC 1.0)|傳回字元字串所組成*string_exp*重複*計數*時間。|  
|**取代 (** *string_exp1*， *string_exp2*， *string_exp3 * * *)** (ODBC 1.0)|搜尋*string_exp1*的 foroccurrences *string_exp2*，並取代*string_exp3*。|  
|**權限 (** *string_exp*，*計數 * * *)** (ODBC 1.0)|傳回最右邊*計數*字元*string_exp*。|  
|**RTRIM (** *string_exp* **)** (ODBC 1.0)|傳回的字元*string_exp*使用尾端空格移除。|  
|**SOUNDEX (** *string_exp* **)** (ODBC 2.0)|傳回資料來源 – 相關的字元字串，代表文字中的音效*string_exp*。 例如，SQL Server 會傳回 4 個數字的 SOUNDEX 代碼。Oracle 會傳回每個字的注音標示表示。|  
|**空間 (** *計數* **)** (ODBC 2.0)|傳回字元字串，其中包含*計數*空格。|  
|**子字串 (** *string_exp*，*啟動*，長度 **)** (ODBC 1.0)|傳回字元字串，衍生自*string_exp*所指定的字元位置開始*啟動*如*長度*字元。|  
|**UCASE (** *string_exp* **)** (ODBC 1.0)|傳回字串中的相等*string_exp*，所有小寫字元轉換成大寫。|
