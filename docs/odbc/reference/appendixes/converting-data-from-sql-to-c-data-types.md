---
title: 將資料從 SQL 轉換為 C 資料類型 |微軟文件
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
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284748"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>將資料從 SQL 轉換成 C 資料類型
當應用程式調用**SQLFetch、SQLFetchScroll**或**SQLGetData**時,驅動程式將從資料源**SQLFetchScroll**檢索數據。 如有必要,它將數據從驅動程式檢索資料的數據類型轉換為**SQLBindCol**或**SQLGetData**中*的目標類型*參數指定的數據類型。 最後,它將數據存儲在**SQLBindCol**或**SQLGetData**中*TargetValuePtr*參數指向的位置(以及 ARD 的SQL_DESC_DATA_PTR欄位)。  
  
 下表顯示了支援的從 ODBC SQL 資料類型到 ODBC C 資料類型的轉換。 填充圓指示 SQL 資料類型的預設轉換(當*TargetType*的值SQL_C_DEFAULT時,資料將轉換為 C 資料類型)。 空心圓表示支援的轉換。  
  
 對於使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式,可能不支援從特定於驅動程式的數據類型轉換。  
  
 轉換資料的格式不受 Windows ® 國家 / 地區設置的影響。  
  
 以下各節中的表描述了驅動程式或數據源如何轉換從數據源檢索到的數據;驅動程式需要支援從它們支援的 ODBC SQL 資料類型轉換為所有 ODBC C 資料類型。 對於給定的 ODBC SQL 資料類型,表的第一列在**SQLBindCol**和**SQLGetData**中列出了*TargetType*參數的合法輸入值。 第二列列出了測試的結果,通常使用**SQLBindCol**或**SQLGetData**中指定的*BufferLength*參數,驅動程式執行該參數以確定是否可以轉換數據。 對於每個結果,第三列和第四列列出放置在*TargetValuePtr*指定的緩衝區中的值,並在驅動程式嘗試轉換數據後在**SQLBindCol**或**SQLGetData**中指定的*StrLen_or_IndPtr*參數。 (StrLen_or_IndPtr*StrLen_or_IndPtr*參數對應於 ARD 的SQL_DESC_OCTET_LENGTH_PTR欄位。最後一列列出了**SQLFetch、SQLFetchScroll****SQLFetch**或**SQLGetData**為每個結果返回的 SQLSTATE。  
  
 如果**SQLBindCol**或**SQLGetData**中*的目標類型*參數包含未在表中顯示給定 ODBC SQL 資料類型的 ODBC C 資料類型的標識符,**則 SQLFetch、SQLFetchScroll**或**SQLGetData**傳**SQLFetchScroll**回 SQLSTATE 07006(受限資料類型屬性衝突)。 如果*TargetType*參數包含一個識別碼,該識別符指定從特定於驅動程式的 SQL 資料類型轉換為 ODBC C 資料類型,並且驅動程式不支援此轉換,**則 SQLFetch、SQLFetchScroll**或**SQLGetData**將傳回 SQLSTATE HYC00(未實現可選功能)。 **SQLFetchScroll**  
  
 儘管表中未顯示該驅動程式,但當 SQL 資料值為 NULL 時,驅動程式將返回*StrLen_or_IndPtr*參數指定的緩衝區中的SQL_NULL_DATA。 有關在進行多次調用以檢索數據時使用*StrLen_or_IndPtr*的說明,請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)函數說明。 將 SQL 資料轉換為字元\*C 數據時 *,StrLen_or_IndPtr*中返回的字元計數不包括空終止位元組。 如果*TargetValuePtr*是空指標 **,SQLGetData**將返回 SQLSTATE HY009(無效使用空指標);在**SQLBindCol**中,這將取消綁定列。  
  
 下表中使用了以下術語和約定:  
  
-   **數據位元組長度**是可在 **TargetValuePtr*中傳回的 C 資料位元組數,無論數據在返回到應用程式之前是否會被截斷。 對於字串資料,這不包括 null 連接端的字元的空間。  
  
-   **字元位元組長度**是以字元格式顯示數據所需的位元組總數。 這是為[「顯示大小」](../../../odbc/reference/appendixes/display-size.md)部分中的每個 C 資料類型定義的,只不過字元位長度以位元組為單位,而顯示大小以字元為單位。  
  
-   *斜體字*中的單詞表示函數參數或 SQL 語法的元素。 有關語法元素的語法,請參閱[附錄 C:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
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
