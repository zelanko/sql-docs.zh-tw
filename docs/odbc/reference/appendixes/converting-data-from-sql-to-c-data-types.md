---
title: "將資料從 SQL 轉換成 C 資料類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8fae054b572cb0d61299781d67adc0038afa9a97
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="converting-data-from-sql-to-c-data-types"></a>將資料從 SQL 轉換成 C 資料類型
當應用程式呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**，驅動程式會從資料來源擷取資料。 如果有需要，它會將資料轉換中的驅動程式擷取它所指定之資料類型的資料型別*TargetType*引數中的**SQLBindCol**或**SQLGetData。** 最後，它將資料儲存在所指位置*TargetValuePtr*引數中的**SQLBindCol**或**SQLGetData** （和 ARD 的 SQL_DESC_DATA_PTR 欄位）。  
  
 下表顯示從 ODBC SQL 的支援的轉換成 ODBC C 資料類型的資料類型。 填滿的圓圈會指示 SQL 資料類型的預設轉換 (C 資料類型的資料將會轉換時的值*TargetType*是 SQL_C_DEFAULT)。 空心圓圈表示是支援的轉換。  
  
 ODBC 3*.x*應用程式使用 ODBC 2。*x*驅動程式，從驅動程式特定資料可能不支援類型轉換。  
  
 已轉換資料的格式不受 Windows® 國家/地區設定。  
  
 下列各節中的資料表描述如何在驅動程式或資料來源將轉換從資料來源; 擷取的資料支援所有 ODBC C 資料類型所支援的 ODBC SQL 資料類型的轉換所需的驅動程式。 為指定的 ODBC SQL 資料類型，資料表的第一個資料行列出的合法的輸入的值*TargetType*引數中的**SQLBindCol**和**SQLGetData**。 第二個資料行列出經常使用的測試結果*Columnsize*引數中指定**SQLBindCol**或**SQLGetData**，若要執行的驅動程式判斷是否可以將轉換的資料。 針對每個結果，第三個和第四個資料行清單放在所指定的緩衝區中的值*TargetValuePtr*和*StrLen_or_IndPtr*引數中指定**SQLBindCol**或**SQLGetData**驅動程式已嘗試將資料轉換之後。 ( *StrLen_or_IndPtr*引數會對應至 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位。)最後一個資料行中列出的每個結果傳回的 SQLSTATE **SQLFetch**， **SQLFetchScroll**，或**SQLGetData**。  
  
 如果*TargetType*引數中的**SQLBindCol**或**SQLGetData**包含 ODBC C 資料類型不會顯示在指定的 ODBC SQL 資料類型的資料表識別碼**SQLFetch**， **SQLFetchScroll**，或**SQLGetData**傳回 SQLSTATE 07006 （受限制的資料類型屬性違規）。 如果*TargetType*引數包含指定從驅動程式專屬 SQL 資料類型轉換為 ODBC C 資料類型的識別項和驅動程式時，不支援這項轉換**SQLFetch**，**SQLFetchScroll**，或**SQLGetData**傳回 SQLSTATE HYC00 （未實作的選擇性功能）。  
  
 雖然它不會顯示在資料表中，驅動程式會傳回所指定的緩衝區的 SQL_NULL_DATA *StrLen_or_IndPtr*引數時，SQL 資料值為 NULL。 如需說明使用的*StrLen_or_IndPtr*時多次呼叫來擷取資料，請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函式描述。 如果 SQL 資料轉換成 C 字元資料，以傳回的字元計數\* *StrLen_or_IndPtr*不包含 null 結束位元組。 如果*TargetValuePtr*為 null 指標， **SQLGetData**傳回 SQLSTATE HY009 （使用無效的 null 指標）; 在**SQLBindCol**，這會解除繫結資料行。  
  
 資料表中使用下列詞彙和慣例：  
  
-   **資料的位元組長度**是可傳回中的 C 資料的位元組數 **TargetValuePtr*是否傳回至應用程式之前，會截斷資料。 字串資料，這不包括 null 結束字元的空間。  
  
-   **字元位元組長度**是以字元格式顯示資料所需的位元組總數。 這是為每個區段中的 C 資料類型所定義的[顯示大小](../../../odbc/reference/appendixes/display-size.md)，不同之處在於字元位元組長度是以位元組為單位的顯示大小是以字元為單位。  
  
-   文字*斜體*代表函式引數或將 SQL 文法的項目。 如需文法項目語法，請參閱[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [SQL 到 c： 字元](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL 到 c： 數字](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL 到 c： 位元](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL 到 c： 二進位](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL 到 c： 日期](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL 到 c: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL 到 c： 時間](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL 到 c： 時間戳記](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL 到 c： 年度月份間隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL 到 c： 日期時間間隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL 到 C 資料轉換範例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)

