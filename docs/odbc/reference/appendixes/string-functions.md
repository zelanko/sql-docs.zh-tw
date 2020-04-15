---
title: 字串函數 :微軟文件
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
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302839"
---
# <a name="string-functions"></a>字串函式
下表列出了字串操作函數。 應用程式可以通過使用*SQL_STRING_FUNCTIONS的資訊類型*呼叫**SQLGetInfo**來確定驅動程式支援哪些字串函數。  
  
## <a name="remarks"></a>備註  
 表示為*string_exp*的參數可以是列的名稱、*字串文本*的名稱或其他標量函數的結果,其中基礎數據類型可以表示為SQL_CHAR、SQL_VARCHAR或SQL_LONGVARCHAR。  
  
 表示為*character_exp*的參數是可變長度字串。  
  
 表示為*起始*、*長度*或*計數*的參數可以是*數位文本*或另一個標量函數的結果,其中基礎數據類型可以表示為SQL_TINYINT、SQL_SMALLINT 或SQL_INTEGER。  
  
 此處列出的字串函數基於 1;也就是說,字串中的第一個字元是字元 1。  
  
 在 ODBC 3.0 中添加了BIT_LENGTH、CHAR_LENGTH、CHARACTER_LENGTH、OCTET_LENGTH 和位置字串標量函數,以便與 SQL-92 對齊。  
  
|函式|描述|  
|--------------|-----------------|  
|**ASCII(** _string_exp_ **)** (ODBC 1.0)|將*string_exp*最左側字元的 ASCII 代碼值作為整數返回。|  
|**BIT_LENGTH(string_exp** _string_exp_ **)** (ODBC 3.0)|傳回字串運算式的長度 (以位元為單位)。<br /><br /> 不僅適用於字串數據類型,因此不會隱式地將*string_exp*轉換為字串,而是返回它所提供的任何數據類型的(內部)大小。|  
|**CHAR(**_程式碼_ **)(ODBC** 1.0)|傳回具有*代碼*指定的 ASCII 代碼值的字元。 代碼的值應介於 0 和 255 之間;*代碼*的值應介於 0 和 255 之間。否則,返回值與數據源相關。|  
|**CHAR_LENGTH(** _string_exp_ **)** (ODBC 3.0)|如果字串表達式是字元數據類型,則返回字串表達式的長度。否則,返回字串表達式的長度(最小整數不小於除以8的位數)。 (此函數與CHARACTER_LENGTH函數相同。|  
|**CHARACTER_LENGTH (string_exp** _string_exp_ **)** (ODBC 3.0)|如果字串表達式是字元數據類型,則返回字串表達式的長度。否則,返回字串表達式的長度(最小整數不小於除以8的位數)。 (此函數與CHAR_LENGTH函數相同。|  
|**CONCAT(string_exp1,string_exp2)** _ _(ODBC 1.0)_ _ ** **|返回將*string_exp2*串聯到*string_exp1*的結果的字串。 產生的字串為 DBMS 相依。 例如,如果由*string_exp1*表示的列包含 NULL 值,DB2 將傳回 NULL,但 SQL Server 將傳回非 NULL 字串。|  
|**差異**_(string_exp1,string_exp2__string_exp2_**)** (ODBC 2.0)|返回一個整數值,指示 SOUNDEX 函數為*string_exp1*和*string_exp2*返回的值之間的差異。|  
|**插入**_(string_exp1,_*開始*,*長度*, _string_exp2_**)** (ODBC 1.0)|傳回一個字串,其中*長度*字元從*string_exp1(**從開始)* 開始刪除,*並且從**開始*將string_exp2插入到*string_exp中*。|  
|**LCASE(** _string_exp_ **)** (ODBC 1.0)|返回一個等於*string_exp*中的字串,所有大寫字元都轉換為小寫。|  
|**左(string_exp,** _ __計數_**)** (ODBC 1.0)|返回*string_exp*的最*左側計數*字元。|  
|**長度 (string_exp** _string_exp_ **)(ODBC** 1.0)|傳回string_exp中的字元數 *,* 不包括尾隨空格。<br /><br /> **長度**僅接受字串。 因此,將隱式*string_exp*轉換為字串,並返回此字串的長度(而不是數據類型的內部大小)。|  
|**位置(string_exp1** _string_exp1_ *,string_exp2*[,*開始***]** (ODBC 1.0)|返回*string_exp2**中第*一次string_exp1的起始位置。 除非指定了可選參數*start*,否則string_exp1的第一次出現*string_exp1的搜索*從*string_exp2*中的第一個字元位置開始。 若指定*了「 開始」 則*搜尋以開始值指示的字元*位置 。* *string_exp2*中的第一個字元位置由值 1 指示。 如果在*string_exp2*內找不到*string_exp1,* 則傳回值 0。<br /><br /> 如果應用程式可以使用*string_exp1**string_exp1、string_exp2*呼叫LOCATE標量函數和*啟動*參數呼叫,則當使用SQL_STRING_FUNCTIONS*選項*呼叫**SQLGetInfo**時,驅動程式將返回SQL_FN_STR_LOCATE。 如果應用程式只能使用*string_exp1*和*string_exp2*參數呼叫 LOCATE 標量函數,則當使用 SQL_STRING_FUNCTIONS*選項*呼叫**SQLGetInfo**時,驅動程式將返回SQL_FN_STR_LOCATE_2。 支援使用兩個或三個參數調用 LOCATE 函數的驅動程式返回SQL_FN_STR_LOCATE和SQL_FN_STR_LOCATE_2。|  
|**LTRIM(** _string_exp_ **)** (ODBC 1.0)|返回*string_exp*的字元,刪除前導空格。|  
|**OCTET_LENGTH(string_exp** _string_exp_ **)** (ODBC 3.0)|傳回字串運算式的長度 (以位元組為單位)。 結果就是不小於位元數的最小整數除以 8。<br /><br /> 不僅適用於字串數據類型,因此不會隱式地將*string_exp*轉換為字串,而是返回它所提供的任何數據類型的(內部)大小。|  
|**位置**_(character_expcharacter_exp_ **IN** _ _ **)** (ODBC 3.0)|返回第二個字元表達式中第一個字元表達式的位置。 結果是一個精確數值,實現定義的精度和比例為 0。|  
|**重**_覆 (string_exp,__計數_**)(ODBC** 1.0)|返回由*重複**計數*string_exp組成的字串。|  
|**取代**_string_exp1_(string_exp1、string_exp2、string_exp3) (ODBC 1.0) _string_exp3_ **)** *string_exp2*|搜尋*string_exp1string_exp2**發生,* 然後取代為*string_exp3。*|  
|**右邊 (string_exp** _ _,_計數_**)** (ODBC 1.0)|返回*string_exp*的最右側*計數*字元。|  
|**RTRIM(** _string_exp_ **)** (ODBC 1.0)|返回刪除尾隨空格的*string_exp*字元。|  
|**音效 (string_exp** _string_exp_ **)** (ODBC 2.0)|返回一個數據源相關字串,表示*string_exp*中單詞的聲音。 例如,SQL Server 返回 4 位元 SOUNDEX 代碼;Oracle 返回每個單詞的語音表示形式。|  
|**空間 (**_計數_ **)(ODBC** 2.0)|返回由*計數*空間組成的字串。|  
|**SUBSTRING (string_exp,** _ _*開始*, 長度 **)** (ODBC 1.0)|返回從*string_exp*派生的字串,從*長度*字元*的起始*符指定的字元位置開始。|  
|**UCASE** _(string_exp_ **)** (ODBC 1.0)|返回一個等於*string_exp*中的字串,所有小寫字元轉換為大寫。|
