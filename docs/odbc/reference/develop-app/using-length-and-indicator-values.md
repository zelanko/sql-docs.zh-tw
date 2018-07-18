---
title: 使用長度與指標值 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1a59b47c8394187f094b8d7c5e1f15611a8f8ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916663"
---
# <a name="using-length-and-indicator-values"></a>使用長度與指標值
長度/指標緩衝區用來傳遞資料緩衝區或例如 SQL_NULL_DATA 表示資料為 NULL 的特殊指標中資料的位元組長度。 根據函式，會使用它，是 SQLINTEGER 或 SQLSMALLINT 定義長度/指標緩衝區。 因此，需要單一引數來描述它。 如果資料緩衝區 nondeferred 輸入的緩衝區，這個引數包含資料本身的位元組長度或指標值。 它通常會命名為*StrLen_or_Ind*或類似的名稱。 例如，下列程式碼呼叫**SQLPutData**傳遞緩衝區的資料; 位元組長度 (*ValueLen*) 因為直接傳遞資料緩衝區 (*ValuePtr*) 是輸入的緩衝區中。  
  
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
  
 資料緩衝區已延後的輸入的緩衝區、 nondeferred 的輸出緩衝區或輸出緩衝區，如果引數包含長度/指標緩衝區的位址。 它通常會命名為*StrLen_or_IndPtr*或類似的名稱。 例如，下列程式碼呼叫**SQLGetData**擷取完整的資料; 緩衝區的位元組長度會傳回到長度/指標緩衝區中的應用程式 (*ValueLenOrInd*)，其位址傳遞至**SQLGetData**因為對應的資料緩衝區 (*ValuePtr*) 是 nondeferred 的輸出緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非特別禁止，長度/指標緩衝區引數可以是 0 (如果 nondeferred 的輸入) 或 null 指標 (如果輸出或延後的輸入)。 輸入緩衝區，這會導致要忽略資料的位元組長度的驅動程式。 這將可變長度資料時傳回錯誤，但時很常見傳遞非 null 的固定長度資料，因為長度指標值就不需要與。 輸出緩衝區，這會使驅動程式不會傳回的資料或指標值的位元組長度。 如果是 NULL，但是時很常見擷取固定長度、 不可為 null 的資料，因為長度指標值就不需要與驅動程式所傳回的資料，這是錯誤。  
  
 因為當延後的資料緩衝區的位址傳遞至驅動程式時，可將延遲的長度/指標緩衝區的位址必須維持有效，直到緩衝區未繫結。  
  
 下列的長度是有效的長度/指標值：  
  
-   *n*，其中*n* > 0。  
  
-   0.  
  
-   SQL_NTS。 字串傳送至對應的資料緩衝區中的驅動程式是以 null 結束。這是 C 程式設計人員，傳遞字串，而不需要計算其位元組長度的便利方式。 只有在應用程式將資料傳送至驅動程式時，這個值會是合法。 當驅動程式傳回資料給應用程式時，一律會傳回資料的實際位元組長度。  
  
 下列是有效值為長度/指標值。 SQL_NULL_DATA 會儲存在 SQL_DESC_INDICATOR_PTR 描述項欄位。所有其他值會儲存在 SQL_DESC_OCTET_LENGTH_PTR 描述項欄位。  
  
-   SQL_NULL_DATA。 資料是 NULL 資料值，並會忽略在對應的資料緩衝區中的值。 此值為合法只能針對 SQL 資料傳送至資料庫或從 驅動程式擷取。  
  
-   SQL_DATA_AT_EXEC。 資料緩衝區不會包含任何資料。 相反地，您會將資料傳送與**SQLPutData**陳述式或當**SQLBulkOperations**或**SQLSetPos**呼叫。 此值為合法只能針對 SQL 資料傳送至驅動程式。 如需詳細資訊，請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集。 這個值是類似於 SQL_DATA_AT_EXEC。 如需詳細資訊，請參閱[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驅動程式無法判斷仍可傳回的輸出緩衝區中的長資料的位元組數目。 此值為合法只能針對從驅動程式擷取 SQL 資料。  
  
-   SQL_DEFAULT_PARAM。 程序是使用輸入參數的預設值，而不是對應的資料緩衝區中值的程序中。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulkOperations**或**SQLSetPos**是要略過的資料緩衝區中的值。 呼叫更新資料列時**SQLBulkOperations**或**SQLSetPos**不會變更資料行值。 插入新的資料列呼叫時**SQLBulkOperations**，資料行值設定為其預設值或資料行沒有預設值為 NULL。
