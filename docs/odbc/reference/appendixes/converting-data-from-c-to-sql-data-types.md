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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fb707e77df7d793277d4a23146adc980eede6fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304657"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>將資料從 C 轉換成 SQL 資料類型
當應用程式呼叫**SQLExecute**或**SQLExecDirect**時，此驅動程式會從應用程式中的儲存位置，抓取任何與**SQLBindParameter**系結之參數的資料。 當應用程式呼叫**SQLSetPos**時，驅動程式會從與**SQLBindCol**系結的資料行抓取更新或加入作業的資料。 對於資料執行中參數，應用程式會使用**SQLPutData**傳送參數資料。 如有必要，驅動程式會將**SQLBindParameter**中*ValueType*引數所指定之資料類型的資料，轉換為**SQLBindParameter**中的*ParameterType*引數所指定的資料類型，然後將資料傳送至資料來源。  
  
 下表顯示從 ODBC C 資料類型到 ODBC SQL 資料類型的支援轉換。 實心圓圈表示 SQL 資料類型的預設轉換（當*ValueType*的值或 SQL_DESC_CONCISE_TYPE 描述項欄位 SQL_C_DEFAULT 時，資料會轉換成的 C 資料類型）。 空心圓形表示支援的轉換。  
  
 已轉換資料的格式不會受到 Windows®國家（地區）設定的影響。  
  
 ![支援的轉換：ODBC C 至 SQL 資料類型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 下列各節中的資料表描述驅動程式或資料來源如何轉換傳送至資料來源的資料;需要驅動程式才能支援從所有 ODBC C 資料類型到其支援的 ODBC SQL 資料類型的轉換。 若為指定的 ODBC C 資料類型，資料表的第一欄會列出**SQLBindParameter**中*ParameterType*引數的合法輸入值。 第二個數據行列出驅動程式執行的測試結果，以判斷它是否可以轉換資料。 第三個數據行會列出**SQLExecDirect**、 **SQLExecute**、 **SQLBulkOperations**、 **SQLSetPos**或**SQLPutData**針對每個結果所傳回的 SQLSTATE。 只有在傳回 SQL_SUCCESS 時，才會將資料傳送至資料來源。  
  
 如果**SQLBindParameter**中的*ParameterType*引數包含在給定 C 資料類型的資料表中未顯示之 ODBC SQL 資料類型的識別碼，則**SQLBindParameter**會傳回 SQLSTATE 07006 （限制的資料類型屬性違規）。 如果*ParameterType*引數包含驅動程式專屬的識別碼，而驅動程式不支援從特定的 ODBC C 資料類型轉換成該驅動程式特定的 SQL 資料類型，則**SQLBINDPARAMETER**會傳回 SQLSTATE HYC00 （未執行的選擇性功能）。  
  
 如果**SQLBindParameter**中指定的*ParameterValuePtr*和*StrLen_or_IndPtr*引數都是 null 指標，則該函式會傳回 SQLSTATE HY009 （不正確 null 指標用法）。 雖然它不會顯示在資料表中，但應用程式會將**SQLBindParameter**的*StrLen_or_IndPtr*引數所指向的長度/指標緩衝區值，或**SQLPutData**的*StrLen_or_IndPtr*引數值設定為 SQL_Null_DATA 以指定 Null SQL 資料值。 （ *StrLen_or_IndPtr*引數會對應至 APD 的 [SQL_DESC_OCTET_LENGTH_PTR] 欄位）。應用程式會將這些值設定為 SQL_NTS 以指定**SQLPutData**中\* **SQLBindParameter**或\* *DataPtr*中*ParameterValuePtr*的值（由 APD 的 SQL_DESC_DATA_PTR 欄位所指向）是以 null 結束的字串。  
  
 下列是在資料表中使用的詞彙：  
  
-   **資料的位元組長度**-可用來傳送至資料來源之 SQL 資料的位元組數目，不論資料是否會在傳送至資料來源之前截斷。 針對字串資料，這不包含 null 終止字元的空間。  
  
-   資料**行位元組長度**-將資料儲存在資料來源所需的位元組數目。  
  
-   **字元位元組長度**-以字元形式顯示資料所需的最大位元組數目。 這是針對 [[顯示大小](../../../odbc/reference/appendixes/display-size.md)] 中的每個 SQL 資料類型所定義，但 [字元位元組長度] 是以位元組為單位，而顯示大小為 [字元]。  
  
-   **位數**-用來表示數位的字元數，包括負號、小數點和指數（如有需要）。  
  
-   **中的單字**   
     ***斜體***-SQL 文法的元素。 如需文法元素的語法，請參閱[附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
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
