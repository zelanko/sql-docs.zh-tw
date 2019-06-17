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
manager: craigg
ms.openlocfilehash: 442d0865ede4819ea3413d662411295daa5b48bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501109"
---
# <a name="using-length-and-indicator-values"></a>使用長度與指標值
長度/指標緩衝區用來傳遞資料緩衝區或例如 SQL_NULL_DATA 表示資料為 NULL 的特殊指標中資料的位元組長度。 根據函式中使用，是 SQLINTEGER 或 SQLSMALLINT 定義長度/指標緩衝區。 因此，需要單一引數，才能加以描述。 如果 nondeferred 的輸入的緩衝區的資料緩衝區，這個引數會包含資料本身的位元組長度或指標值。 它通常會命名為*Strlen_or_ind&lt*或其他類似的名稱。 例如，下列程式碼會呼叫**SQLPutData**傳遞緩衝區完整的資料; 的位元組長度 (*ValueLen*) 因為直接傳遞的資料緩衝區 (*ValuePtr*) 是輸入的緩衝區。  
  
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
  
 如果延後的輸入的緩衝區、 nondeferred 的輸出緩衝區中或輸出緩衝區的資料緩衝區，引數會包含長度/指標緩衝區的位址。 它通常會命名為*StrLen_or_IndPtr*或其他類似的名稱。 例如，下列程式碼會呼叫**SQLGetData**擷取完整的資料; 緩衝區的位元組長度會傳回到之長度/指標緩衝區中的應用程式 (*ValueLenOrInd*)，其位址是傳遞給**SQLGetData**因為對應的資料緩衝區 (*ValuePtr*) nondeferred 的輸出緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非特別禁止，長度/指標緩衝區引數可以是 0 (如果 nondeferred 的輸入) 或 null 指標 (如果輸出或延後的輸入)。 輸入緩衝區，這會導致驅動程式略過資料的位元組長度。 這會傳遞可變長度的資料時，會傳回錯誤，但常見於時傳遞非 null 的固定長度資料，因為長度的指標值就不需要與。 輸出緩衝區，這會導致驅動程式不會傳回的資料或指標值的位元組長度。 如果是 NULL，但是常見於時擷取固定長度、 不可為 null 的資料，因為長度的指標值就不需要與驅動程式所傳回的資料，這會是錯誤。  
  
 因為時延遲的資料緩衝區的位址傳遞至驅動程式時，延後的長度/指標緩衝區的位址必須保持有效，直到緩衝區未繫結。  
  
 下列的長度是有效的長度/指標值：  
  
-   *n*，其中*n* > 0。  
  
-   0.  
  
-   SQL_NTS. 傳送至對應的資料緩衝區中的驅動程式的字串是以 null 終止;這是便利的方式，為 C 程式設計人員將不用來計算其位元組長度的字串。 此值在應用程式會將資料傳送至驅動程式時，才是合法的。 當驅動程式會回到應用程式中的資料時，它一律會傳回資料的實際位元組長度。  
  
 下列是有效值做為長度/指標值。 SQL_NULL_DATA 會儲存在 SQL_DESC_INDICATOR_PTR 描述項欄位;所有其他值會儲存在 SQL_DESC_OCTET_LENGTH_PTR 描述項欄位。  
  
-   SQL_NULL_DATA. 資料為 NULL 的資料值，並會忽略對應的資料緩衝區中的值。 這個值是合法的只能針對 SQL 資料傳送至或擷取來自驅動程式。  
  
-   SQL_DATA_AT_EXEC. 資料緩衝區不包含任何資料。 相反地，您會將資料傳送與**SQLPutData**陳述式執行時，或當**SQLBulkOperations**或是**SQLSetPos**呼叫。 這個值是合法的只能針對 SQL 資料傳送至驅動程式。 如需詳細資訊，請參閱 < [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，並[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集。 這個值是類似於 SQL_DATA_AT_EXEC。 如需詳細資訊，請參閱 <<c0> [ 傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驅動程式無法判斷傳回的輸出緩衝區中仍然可用的長資料的位元組數目。 這個值是合法的只能針對 SQL 資料擷取的驅動程式。  
  
-   SQL_DEFAULT_PARAM. 程序是使用中的程序，而不是對應的資料緩衝區中值的輸入參數的預設值。  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations**或是**SQLSetPos**要忽略的資料緩衝區中的值。 藉由呼叫更新的資料列時**SQLBulkOperations**或是**SQLSetPos**不會變更資料行的值。 藉由呼叫插入新的資料列時**SQLBulkOperations**，資料行的值設為其預設值或資料行沒有預設值，為 NULL。
