---
title: 將資料從 C 轉換為 SQL 資料類型 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304657"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>將資料從 C 轉換成 SQL 資料類型
當應用程式呼叫**SQLExecute**或**SQLExecDirect**時,驅動程式從應用程式中的儲存位置檢索與**SQLBind 參數**綁定的任何參數的數據。 當應用程式呼叫**SQLSetPos**時,驅動程式檢索更新的數據,或從綁定**到 SQLBindCol**的列中添加操作。 對於執行時的數據參數,應用程式使用**SQLPutData**發送參數數據。 如有必要,驅動程式將數據從**SQLBind 參數**中*ValueType*參數指定的數據類型轉換為**SQLBind 參數**中的*參數類型*參數指定的數據類型,然後將數據發送到數據源。  
  
 下表顯示了支援的從 ODBC C 資料類型到 ODBC SQL 資料類型的轉換。 填充圓指示 SQL 資料類型的預設轉換(當*ValueType*的值或SQL_DESC_CONCISE_TYPE描述符欄位SQL_C_DEFAULT時,將轉換數據的 C 資料類型)。 空心圓表示支援的轉換。  
  
 轉換資料的格式不受 Windows ® 國家 / 地區設置的影響。  
  
 ![支援的轉換：ODBC C 至 SQL 資料類型](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 以下各節中的表描述了驅動程式或數據源如何轉換發送到數據源的數據;需要驅動程式來支援從所有 ODBC C 資料類型轉換為他們支援的 ODBC SQL 資料類型。 對於給定的 ODBC C 資料類型,表的第一列在**SQLBind 參數**中列出了*參數類型*參數的合法輸入值。 第二列列出了驅動程式執行以確定是否可以轉換數據的測試的結果。 第三列列出了 SQLExecDirect、SQLExecute、SQLBulk**操作****、SQLSetPos**或**SQLPutData**為每個結果傳**SQLExecDirect****SQLExecute**回的 SQLSTATE。 僅當返回SQL_SUCCESS時,才會將數據發送到數據源。  
  
 如果**SQLBind 參數**中的*參數類型*參數包含未在給定 C 資料類型的表中顯示的 ODBC SQL 資料類型的識別碼,則**SQLBind 參數**將傳回 SQLSTATE 07006(受限資料類型屬性衝突)。 如果*參數類型*參數包含特定於驅動程式的識別碼,並且驅動程式不支援從特定的 ODBC C 資料類型轉換為該驅動程式特定的 SQL 資料類型,**則 SQLBind 參數**將傳回 SQLSTATE HYC00(未實現可選功能)。  
  
 如果**SQLBind 參數**中指定的*參數 ValuePtr*和*StrLen_or_IndPtr*參數都是空指標,則該函數將返回 SQLSTATE HY009(無效使用空指標)。 儘管表中未顯示,但應用程式會設置**SQLBind 參數***StrLen_or_IndPtr*參數指向的長度/ 指示器緩衝區的值,或者**SQLPutData** *StrLen_or_IndPtr*參數的值SQL_NULL_DATA以指定 NULL SQL 資料值。 (StrLen_or_IndPtr*StrLen_or_IndPtr*參數對應於 APD 的SQL_DESC_OCTET_LENGTH_PTR欄位。應用程式將這些值設置為SQL_NTS,以指定**SQLBind**\*參數 或**SQLPutData**中的\**DataPtr*中的*參數 ValuePtr*中的值(由 APD 的SQL_DESC_DATA_PTR字段指向)是一個空端字串。  
  
 下表中使用了以下術語:  
  
-   **數據位元組長度**- 可用於發送到資料來源的 SQL 資料位元組數,無論資料在發送到資料來源之前是否會被截斷。 對於字串資料,這不包括 null 終止字元的空間。  
  
-   **欄位長度**- 將資料儲存在資料來源中所需的位元組數。  
  
-   **字元位元組長度**- 以字元形式顯示資料所需的最大位元組數。 這是為[顯示大小](../../../odbc/reference/appendixes/display-size.md)中的每個 SQL 數據類型定義的,但字元位元組長度以位元組為單位,而顯示大小以字元為單位。  
  
-   **數位數**- 用於表示數位的字元數,包括減號、小數點和指數(如果需要)。  
  
-   **單詞在**   
     ***斜體***- SQL 語法的元素。 有關語法元素的語法,請參閱[附錄 C:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。  
  
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
