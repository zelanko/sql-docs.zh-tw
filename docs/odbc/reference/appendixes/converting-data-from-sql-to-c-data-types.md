---
description: 將資料從 SQL 轉換成 C 資料類型
title: 將資料從 SQL 轉換成 C 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c1306564a9e4a5c1cbd9cac74508529a1e6df9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429690"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>將資料從 SQL 轉換成 C 資料類型
當應用程式呼叫 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData**時，驅動程式會從資料來源中取出資料。 如果有需要，它會將資料從驅動程式抓取資料的資料類型轉換為**SQLBindCol**或 SQLGetData 中的*TargetType*引數所指定的資料類型 **。** 最後，它會將資料儲存在**SQLBindCol**或**SQLGetData** (中的*TargetValuePtr*引數所指向的位置，以及 ARD) 的 SQL_DESC_DATA_PTR 欄位。  
  
 下表顯示從 ODBC SQL 資料類型到 ODBC C 資料類型的支援轉換。 實心圓圈表示 SQL 資料類型的預設轉換 (當 *TargetType* 的值是 SQL_C_DEFAULT) 時，資料會轉換成的 C 資料類型。 空心圓圈表示支援的轉換。  
  
 如果 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式，則可能不支援從驅動程式特定的資料類型進行轉換。  
  
 已轉換資料的格式不受 Windows® country 設定的影響。  
  
 下列各節中的表格描述驅動程式或資料來源如何轉換從資料來源取出的資料;需要有驅動程式，才能支援從支援的 ODBC SQL 資料類型轉換成所有的 ODBC C 資料類型。 針對給定的 ODBC SQL 資料類型，資料表的第一個資料行會列出**SQLBindCol**和**SQLGetData**中*TargetType*引數的合法輸入值。 第二個數據行列出測試的結果，通常使用**SQLBindCol**或**SQLGetData**中指定的*BufferLength*引數，驅動程式會執行此引數來判斷是否可以轉換資料。 針對每個結果，第三個和第四個數據行會列出在驅動程式嘗試轉換資料之後，在**SQLBindCol**或**SQLGetData**中指定的*TargetValuePtr*和*StrLen_or_IndPtr*引數所指定之緩衝區中所放置的值。  (*StrLen_or_IndPtr* 引數對應至 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位。 ) 最後一個資料行會列出 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData**的每個結果所傳回的 SQLSTATE。  
  
 如果**SQLBindCol**或**SQLGetData**中的*TargetType*引數包含未在給定 odbc SQL 資料類型的資料表中顯示之 ODBC C 資料類型的識別碼，則**SQLFETCH**、 **SQLFetchScroll**或**SQLGetData**會傳回 SQLSTATE 07006 (限制的資料類型屬性違規) 。 如果 *TargetType* 引數包含指定從驅動程式特定的 SQL 資料類型轉換為 ODBC C 資料類型的識別碼，且驅動程式、 **SQLFetch**、 **SQLFetchScroll**或 **SQLGetData** 不支援此轉換，則會傳回 SQLSTATE HYC00 (未) 執行的選擇性功能。  
  
 雖然不會在資料表中顯示，但是當 SQL 資料值為 Null 時，驅動程式會在 *StrLen_or_IndPtr* 引數所指定的緩衝區中傳回 SQL_Null_DATA。 如需建立多個呼叫來取得資料時使用 *StrLen_or_IndPtr* 的說明，請參閱 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函數描述。 當 SQL 資料轉換成字元 C 資料時，StrLen_or_IndPtr 中傳回的字元計數 \* *StrLen_or_IndPtr*不包括 null 終止位元組。 如果 *TargetValuePtr* 為 null 指標，則 **SQLGETDATA** 會傳回 SQLSTATE HY009 (Null 指標的用法無效) ;在 **SQLBindCol**中，這會將資料行解除系結。  
  
 表格中使用下列詞彙和慣例：  
  
-   **Byte 長度的資料** 是可在 **TargetValuePtr*中傳回的 C 資料位元組數目，不論資料在傳回給應用程式之前，是否會被截斷。 若為字串資料，則不包含 null 終止字元的空間。  
  
-   **字元位元組長度** 是以字元格式顯示資料所需的總位元組數。 這是針對區段 [顯示大小](../../../odbc/reference/appendixes/display-size.md)中的每個 C 資料類型所定義的，但字元位元組長度是以位元組為單位，而顯示大小是以字元為單位。  
  
-   *斜體*的單字表示函式引數或 SQL 文法的元素。 如需文法元素的語法，請參閱 [附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
 此章節包含下列主題。  
  
-   [SQL 到 C：字元](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL 到 C：數值](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL 到 C：位元](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL 到 C：二進位](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL 到 C：日期](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL 到 C：GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL 到 C：時間](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL 到 C：時間戳記](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL 到 C：年月間隔](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL 到 C：日期時間間隔](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL 到 C 資料轉換範例](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
