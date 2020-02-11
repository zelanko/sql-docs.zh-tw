---
title: 使用長度與指標值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67902474"
---
# <a name="using-length-and-indicator-values"></a>使用長度與指標值
長度/指標緩衝區是用來傳遞資料緩衝區中的資料位元組長度或特殊指標（例如 SQL_Null_DATA），這表示資料為 Null。 視使用的函式而定，長度/指標緩衝區會定義為 SQLINTEGER 或 SQLSMALLINT。 因此，需要單一引數來描述它。 如果資料緩衝區是 nondeferred 輸入緩衝區，此引數會包含資料本身的位元組長度或指標值。 它通常會命名為*StrLen_or_Ind*或類似的名稱。 例如，下列程式碼會呼叫**SQLPutData**來傳遞完整資料的緩衝區;位元組長度（*ValueLen*）是直接傳遞的，因為資料緩衝區（*valueptr 是*）是輸入緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 如果資料緩衝區是延後的輸入緩衝區、nondeferred 輸出緩衝區或輸出緩衝區，引數就會包含長度/指標緩衝區的位址。 它通常會命名為*StrLen_or_IndPtr*或類似的名稱。 例如，下列程式碼會呼叫**SQLGetData** ，以取出完整的資料緩衝區;位元組長度會傳回長度/指標緩衝區（*ValueLenOrInd*）中的應用程式，其位址會傳遞至**SQLGetData** ，因為對應的資料緩衝區（*valueptr 是*）是 nondeferred 輸出緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非特別禁止，否則長度/指標緩衝區引數可以是0（如果是 nondeferred 輸入）或 null 指標（如果輸出或延後的輸入）。 對於輸入緩衝區，這會導致驅動程式忽略資料的位元組長度。 這會在傳遞可變長度的資料時傳回錯誤，但在傳遞非 null 的固定長度資料時很常見，因為不需要長度或指標值。 針對輸出緩衝區，這會導致驅動程式不傳回資料的位元組長度或指標值。 如果驅動程式所傳回的資料是 Null，但因為不需要長度或指標值，所以在抓取固定長度、不可為 null 的資料時，這會產生錯誤。  
  
 當延遲資料緩衝區的位址傳遞至驅動程式時，延後長度/指標緩衝區的位址必須維持有效，直到緩衝區解除系結為止。  
  
 下列長度是有效的長度/指標值：  
  
-   *n*，其中*n* > 0。  
  
-   0.  
  
-   SQL_NTS。 在對應的資料緩衝區中傳送到驅動程式的字串會以 null 終止;這是一種方便的方式，讓 C 程式設計人員傳遞字串，而不需要計算其位元組長度。 只有當應用程式將資料傳送至驅動程式時，這個值才是合法的。 當驅動程式將資料傳回給應用程式時，它一律會傳回資料的實際位元組長度。  
  
 下列值是有效的長度/指標值。 SQL_Null_DATA 儲存在 [SQL_DESC_INDICATOR_PTR 描述項] 欄位中;所有其他值都會儲存在 [SQL_DESC_OCTET_LENGTH_PTR 描述項] 欄位中。  
  
-   SQL_Null_DATA。 資料是 Null 資料值，而對應資料緩衝區中的值會被忽略。 此值僅適用于從驅動程式傳送或取出的 SQL 資料。  
  
-   SQL_DATA_AT_EXEC。 資料緩衝區不包含任何資料。 而是在執行語句時，或在呼叫**SQLBulkOperations**或**SQLSetPos**時，使用**SQLPutData**來傳送資料。 此值僅對傳送至驅動程式的 SQL 資料是合法的。 如需詳細資訊，請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果。 這個值類似于 SQL_DATA_AT_EXEC。 如需詳細資訊，請參閱傳送[長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驅動程式無法判斷在輸出緩衝區中仍然可以傳回長資料的位元組數。 此值僅適用于從驅動程式抓取的 SQL 資料。  
  
-   SQL_DEFAULT_PARAM。 程式是在程式中使用輸入參數的預設值，而不是對應資料緩衝區中的值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulkOperations**或**SQLSetPos**是用來忽略資料緩衝區中的值。 藉由呼叫**SQLBulkOperations**或 SQLSetPos 來更新資料列時 **，** 不會變更資料行的值。 當您呼叫**SQLBulkOperations**來插入新的資料列時，會將資料行值設為其預設值，或者，如果資料行沒有預設值，則為 Null。
