---
description: 字串函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42a5301f49a033dbc6e84a5fe43d68c794a76e84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386474"
---
# <a name="string-functions"></a>字串函式
下表列出字串操作函數。 應用程式可以藉由呼叫 SQL_STRING_FUNCTIONS*資訊類型*的**SQLGetInfo** ，判斷驅動程式所支援的字串函數。  
  
## <a name="remarks"></a>備註  
 表示為 *string_exp* 的引數可以是資料行的名稱、 *字元字串常*值或另一個純量函數的結果，其中基礎資料類型可以表示為 SQL_CHAR、SQL_VARCHAR 或 SQL_LONGVARCHAR。  
  
 表示為 *character_exp* 的引數是可變長度的字元字串。  
  
 表示為 *開始*、 *長度*或 *計數* 的引數可以是 *數值常* 值或另一個純量函數的結果，其中基礎資料類型可以表示為 SQL_TINYINT、SQL_SMALLINT 或 SQL_INTEGER。  
  
 此處所列的字串函數是以1為基礎;也就是字串中的第一個字元是字元1。  
  
 ODBC 3.0 中已加入 BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH 和位置字串純量函數，以配合 SQL-92。  
  
|函式|描述|  
|--------------|-----------------|  
|**ASCII (** _STRING_EXP_ **) **  (ODBC 1.0) |以整數形式傳回 *string_exp* 最左邊字元的 ASCII 代碼值。|  
|**BIT_LENGTH (** _STRING_EXP_ **) **  (ODBC 3.0) |傳回字串運算式的長度 (以位元為單位)。<br /><br /> 不只適用于字串資料類型，因此不會以隱含方式將 *string_exp* 轉換成字串，而是會傳回所提供之任何資料類型的 (內部) 大小。|  
|**CHAR (** 程式 _代碼_ **) **  (ODBC 1.0) |傳回包含程式 *代碼*所指定之 ASCII 代碼值的字元。 程式 *代碼* 的值應介於0與255之間;否則，傳回值會與資料來源相依。|  
|**CHAR_LENGTH (** _STRING_EXP_ **) **  (ODBC 3.0) |如果字串運算式是字元資料類型，則傳回字串運算式的長度（以字元為單位）。否則，會傳回字串運算式的長度（以位元組為單位）， (不小於位數除以 8) 的最小整數。  (此函數與 CHARACTER_LENGTH 函數相同。 ) |  
|**CHARACTER_LENGTH (** _STRING_EXP_ **) **  (ODBC 3.0) |如果字串運算式是字元資料類型，則傳回字串運算式的長度（以字元為單位）。否則，會傳回字串運算式的長度（以位元組為單位）， (不小於位數除以 8) 的最小整數。  (此函數與 CHAR_LENGTH 函數相同。 ) |  
|**CONCAT (** _string_exp1_、_string_exp2_ **) ** (ODBC 1.0) |傳回將 *string_exp2* 串連至 *string_exp1*結果的字元字串。 產生的字串為 DBMS 相依。 例如，如果 *string_exp1* 所代表的資料行包含 null 值，則 DB2 會傳回 null，但 SQL Server 會傳回非 Null 字串。|  
|**差異 (** _string_exp1_、_string_exp2_ **) ** (ODBC 2.0) |傳回整數值，指出 SOUNDEX 函數傳回的值與 *string_exp1* 和 *string_exp2*之間的差異。|  
|**INSERT (** _string_exp1_、 *start*、 *length*、 _string_exp2_ **) ** (ODBC 1.0) |傳回字元字串，其中*長度*字元已經從*string_exp1*中刪除，從*開始*，到*string_exp2*插入*string_exp*的位置*開始。*|  
|**LCASE (** _STRING_EXP_ **) ** (ODBC 1.0) |傳回在 *string_exp*中等於該字串，並將所有大寫字元轉換成小寫字元。|  
|**LEFT (** _string_exp_、 _count_ **) ** (ODBC 1.0) |傳回*string_exp*的最左邊*計數*字元。|  
|**長度 (** _STRING_EXP_ **) ** (ODBC 1.0) |傳回 string_exp 中的字元數 *，* 但尾端空白除外。<br /><br /> **長度** 只接受字串。 因此，會將 *string_exp* 隱含地轉換成字串，並傳回此字串的長度， (不是資料類型) 的內部大小。|  
|**找出 (** _string_exp1_， *string_exp2*[， *start*]**) ** (ODBC 1.0) |傳回*string_exp2*中第一次出現*string_exp1*的開始位置。 除非指定了選擇性的引數（ *start*），否則搜尋第一個出現的*string_exp1*開頭會是*string_exp2*中的第一個字元位置。 如果指定了 *start* ，搜尋就會以 *start*值所指出的字元位置開始。 *String_exp2*中的第一個字元位置會以值1表示。 如果在*string_exp2*內找不到*string_exp1* ，則會傳回值0。<br /><br /> 如果應用程式可以使用 *string_exp1*、 *string_exp2*和 *START* 引數來呼叫尋找純量函數，驅動程式會在呼叫 **SQLGetInfo** 時，傳回 SQL_FN_STR_LOCATE SQL_STRING_FUNCTIONS 的 *選項* 。 如果應用程式只能使用*string_exp1*和*string_exp2*引數來呼叫尋找純量函數，則當使用 SQL_STRING_FUNCTIONS 的*選項*呼叫**SQLGetInfo**時，驅動程式會傳回 SQL_FN_STR_LOCATE_2。 支援以兩個或三個引數呼叫尋找函式的驅動程式會同時傳回 SQL_FN_STR_LOCATE 和 SQL_FN_STR_LOCATE_2。|  
|**LTRIM (** _STRING_EXP_ **) ** (ODBC 1.0) |傳回已移除開頭空白的 *string_exp*字元。|  
|**OCTET_LENGTH (** _STRING_EXP_ **) ** (ODBC 3.0) |傳回字串運算式的長度 (以位元組為單位)。 結果就是不小於位元數的最小整數除以 8。<br /><br /> 不只適用于字串資料類型，因此不會以隱含方式將 *string_exp* 轉換成字串，而是會傳回所提供之任何資料類型的 (內部) 大小。|  
|_Character_exp_ **) **中** (** _character_exp_ **的**位置 (ODBC 3.0) |傳回第二個字元運算式中第一個字元運算式的位置。 結果是一個精確的數值，具有實定義的有效位數和一個小數位數0。|  
|**重複 (** _string_exp、_ _count_ **) ** (ODBC 1.0) |傳回由 *string_exp* 重複 *計數* 時間所組成的字元字串。|  
|**取代 (** _string_exp1_、 *string_exp2* _string_exp3_ **) ** (ODBC 1.0) |搜尋 *string_exp1* 的 *string_exp2*foroccurrences，並以 *string_exp3*取代。|  
|**RIGHT (** _string_exp_、 _count_ **) ** (ODBC 1.0) |傳回*string_exp*的最右邊*計數*字元。|  
|**RTRIM (** _STRING_EXP_ **) ** (ODBC 1.0) |傳回已移除尾端空白的 *string_exp* 字元。|  
|**SOUNDEX (** _STRING_EXP_ **) ** (ODBC 2.0) |傳回資料來源相依的字元字串，代表 *string_exp*中的單字音效。 例如，SQL Server 會傳回4位數的 SOUNDEX 代碼;Oracle 會傳回每個單字的語音標記法。|  
|**) ** (ODBC 2.0) 的**空間 (** _計數_|傳回由 *計數* 空間組成的字元字串。|  
|**子字串 (** _string_exp_、 *開始*、長度 **) ** (ODBC 1.0) |傳回從*string_exp*開始的字元字串，從*長度*字元*開頭*指定的字元位置開始。|  
|**UCASE (** _STRING_EXP_ **) ** (ODBC 1.0) |傳回在 *string_exp*中等於該字串，並將所有小寫字元轉換成大寫字元。|
