---
title: 將資料從 C 轉換成 SQL 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f68b53dd77305163aa2595c60a1994a13bb9964
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793806"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>將資料從 C 轉換成 SQL 資料類型
當應用程式呼叫**SQLExecute**或是**SQLExecDirect**，驅動程式會針對與任何參數繫結，擷取資料**SQLBindParameter**中的儲存體位置應用程式。 當應用程式呼叫**SQLSetPos**，驅動程式擷取更新的資料，或加入作業無法使用繫結的資料行**SQLBindCol**。 資料在執行中參數，如應用程式傳送的參數資料**SQLPutData**。 如果有必要，驅動程式會將資料轉換所指定之資料類型從*ValueType*中的引數**SQLBindParameter**所指定的資料型別*ParameterType*中的引數**SQLBindParameter**，然後將資料傳送至資料來源。  
  
 下表顯示支援的轉換，從 ODBC C 資料類型與 ODBC SQL 資料類型。 區域分布的圓圈會指示 SQL 資料類型的預設轉換 (C 資料類型的資料會轉換時的值*ValueType* SQL_DESC_CONCISE_TYPE 描述項欄位是 SQL_C_DEFAULT 或)。 空心圓表示支援的轉換。  
  
 已轉換的資料格式不會受到 Windows® 國家/地區設定。  
  
 ![支援的轉換： ODBC C 至 SQL 資料類型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 下列各節中的資料表描述驅動程式或資料來源將資料傳送至資料來源;支援從所有的 ODBC C 資料類型轉換為其所支援的 ODBC SQL 資料類型所需的驅動程式。 指定的 ODBC C 資料類型，資料表的第一個資料行列出的合法的輸入的值*ParameterType*中的引數**SQLBindParameter**。 第二個資料行中列出驅動程式會判斷如果它可以將資料轉換執行的測試的結果。 第三個資料行列出每個結果所傳回的 SQLSTATE **SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**， **SQLSetPos**，或**SQLPutData**。 資料會傳送至資料來源中，才會傳回 SQL_SUCCESS。  
  
 如果*ParameterType*中的引數**SQLBindParameter**包含不會顯示在指定的 C 資料類型，資料表中的 ODBC SQL 資料類型的識別碼**SQLBindParameter**會傳回 SQLSTATE 07006 （受限制的資料類型屬性違規）。 如果*ParameterType*引數中包含的驅動程式特定識別項和驅動程式不支援從特定的 ODBC C 資料類型轉換為該特定驅動程式，SQL 資料型別**SQLBindParameter**會傳回 SQLSTATE HYC00 （未實作選擇性功能）。  
  
 如果*ParameterValuePtr*並*StrLen_or_IndPtr*中指定的引數**SQLBindParameter**都是 null 指標，函式會傳回 SQLSTATE HY009 （不正確使用 null 指標）。 雖然它未顯示在資料表中，應用程式設定的值所指向之長度/指標緩衝區*StrLen_or_IndPtr*引數**SQLBindParameter**的值或*StrLen_or_IndPtr*引數**SQLPutData**為 SQL_NULL_DATA，若要指定 NULL 的 SQL 資料值。 ( *StrLen_or_IndPtr*引數會對應至 APD 中的 SQL_DESC_OCTET_LENGTH_PTR 欄位。)應用程式設定這些值來指定 sql_nts; 中的值\* *ParameterValuePtr*中**SQLBindParameter**或是\* *DataPtr*中**SQLPutData** （由指向 APD 的 SQL_DESC_DATA_PTR 欄位） 是以 null 結束的字串。  
  
 在資料表中使用下列詞彙：  
  
-   **資料的位元組長度**— 可傳送至資料來源，是否將截斷資料，傳送到資料來源之前的 SQL 資料的位元組數目。 針對字串資料，這不包括 null 結束字元的空間。  
  
-   **資料行的位元組長度**— 儲存在資料來源的資料所需的位元組數目。  
  
-   **字元的位元組長度**— 字元形式來顯示資料所需的位元組數目上限。 這是針對每個 SQL 資料類型所定義[顯示大小](../../../odbc/reference/appendixes/display-size.md)，但字元位元組長度是以位元組為單位，而顯示大小是以字元為單位。  
  
-   **數字數目**— 用來表示數字，包括負號、 小數點和指數 （如有需要） 的字元數。  
  
-   **中的文字**   
     ***斜體***— SQL 文法的項目。 如需語法的文法項目，請參閱[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [C 到 SQL：字元](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C 到 SQL：數值](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C 到 SQL：位元](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C 到 SQL：二進位](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C 到 SQL：日期](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C 到 SQL：GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C 到 SQL：時間](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C 到 SQL：時間戳記](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C 到 SQL：年月間隔](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C 到 SQL：日期時間間隔](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [C 到 SQL 資料轉換範例](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
