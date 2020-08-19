---
description: 將資料從 C 轉換成 SQL 資料類型
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
ms.openlocfilehash: 56af1e376edffa0268a2e27c840f035e5cda9763
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429710"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>將資料從 C 轉換成 SQL 資料類型
當應用程式呼叫 **SQLExecute** 或 **SQLExecDirect**時，驅動程式會從應用程式中的儲存位置，抓取任何與 **SQLBindParameter** 系結之參數的資料。 當應用程式呼叫 **SQLSetPos**時，驅動程式會從以 **SQLBindCol**系結的資料行中抓取更新或新增作業的資料。 針對資料執行中參數，應用程式會使用 **SQLPutData**傳送參數資料。 必要時，驅動程式會將資料從**SQLBindParameter**中的*ValueType*引數所指定的資料類型，轉換為**SQLBindParameter**中*ParameterType*引數所指定的資料類型，然後將資料傳送到資料來源。  
  
 下表顯示從 ODBC C 資料類型到 ODBC SQL 資料類型的支援轉換。 實心圓圈表示 SQL 資料類型的預設轉換， (當 *ValueType* 或 SQL_DESC_CONCISE_TYPE 描述項欄位的值 SQL_C_DEFAULT) 時，資料將轉換成的 C 資料類型。 空心圓圈表示支援的轉換。  
  
 已轉換資料的格式不受 Windows® country 設定的影響。  
  
 ![支援的轉換：ODBC C 至 SQL 資料類型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 下列各節中的表格描述驅動程式或資料來源如何轉換傳送到資料來源的資料;需要有驅動程式，才能支援從所有 ODBC C 資料類型轉換成支援的 ODBC SQL 資料類型。 針對給定的 ODBC C 資料類型，資料表的第一個資料行會列出**SQLBindParameter**中*ParameterType*引數的合法輸入值。 第二個數據行列出驅動程式執行的測試結果，以判斷它是否可以轉換資料。 第三個數據行會列出 **SQLExecDirect**、 **SQLExecute**、 **SQLBulkOperations**、 **SQLSetPos**或 **SQLPutData**的每個結果所傳回的 SQLSTATE。 只有在傳回 SQL_SUCCESS 時，才會將資料傳送到資料來源。  
  
 如果**SQLBindParameter**中的*ParameterType*引數包含未在指定 C 資料類型的資料表中顯示之 ODBC SQL 資料類型的識別碼，則**SQLBindParameter**會傳回 SQLSTATE 07006 (限制的資料類型屬性違規) 。 如果 *ParameterType* 引數包含驅動程式專屬的識別碼，而驅動程式不支援從特定的 ODBC C 資料類型轉換為該驅動程式特定的 SQL 資料類型，則 **SQLBINDPARAMETER** 會傳回 SQLSTATE HYC00 (選用功能未) 執行。  
  
 如果在**SQLBindParameter**中指定的*ParameterValuePtr*和*StrLen_or_IndPtr*引數都是 null 指標，該函式會傳回 SQLSTATE HY009 (不正確使用 null 指標) 。 雖然不會在資料表中顯示，但應用程式會將**SQLBindParameter**的*StrLen_or_IndPtr*引數所指向的長度/指標緩衝區值，或**SQLPutData**的*StrLen_or_IndPtr*引數值設定為 SQL_Null_DATA，以指定 Null SQL 資料值。  (*StrLen_or_IndPtr*引數會對應至 APD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位。 ) 應用程式將這些值設定為 SQL_NTS，以指定 \* SQLPutData (之 APD SQL_DESC_DATA_PTR**中** *ParameterValuePtr*的值 \* *DataPtr*是以 null 結束的字串。 **SQLPutData**  
  
 表格中使用下列詞彙：  
  
-   **位元組長度的資料** -可用來傳送到資料來源的 SQL 資料位元組數目，資料在傳送到資料來源之前，是否會被截斷。 若為字串資料，則不包含 null 終止字元的空間。  
  
-   資料**行位元組長度**-在資料來源中儲存資料所需的位元組數目。  
  
-   **字元位元組長度** -以字元形式顯示資料所需的最大位元組數目。 這是針對 [顯示大小](../../../odbc/reference/appendixes/display-size.md)中的每個 SQL 資料類型所定義，但字元位元組長度是以位元組為單位，而顯示大小是以字元為單位。  
  
-   **數位數目-用** 來表示數位的字元數，包括減號、小數點和指數 (視需要) 。  
  
-   **中的單字**   
     ***斜體***  -SQL 文法的元素。 如需文法元素的語法，請參閱 [附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
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
