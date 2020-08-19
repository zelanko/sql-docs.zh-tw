---
description: 使用長度與指標值
title: 使用長度和指標值 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9c7feb463b2a92d716be24c76d00b64c69a860
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424400"
---
# <a name="using-length-and-indicator-values"></a>使用長度與指標值
長度/指標緩衝區可用來傳遞資料緩衝區中資料的位元組長度或特殊指標，例如 SQL_Null_DATA，這表示資料為 Null。 根據使用它的函式，長度/指標緩衝區會定義為 SQLINTEGER 或 SQLSMALLINT。 因此，需要單一引數來描述它。 如果資料緩衝區是 nondeferred 輸入緩衝區，此引數會包含資料本身的位元組長度或指標值。 它通常名為 *StrLen_or_Ind* 或類似的名稱。 例如，下列程式碼會呼叫**SQLPutData**來傳遞大量資料的緩衝區;因為資料緩衝區 (*ValuePtr*) 是輸入緩衝區，所以會直接傳遞 (*ValueLen*) 的位元組長度。  
  
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
  
 如果資料緩衝區是延後的輸入緩衝區、nondeferred 輸出緩衝區或輸出緩衝區，則引數會包含長度/指標緩衝區的位址。 它通常名為 *StrLen_or_IndPtr* 或類似的名稱。 例如，下列程式碼會呼叫 **SQLGetData** 來取出資料的緩衝區，位元組長度會傳回長度/指標緩衝區中的應用程式 (*ValueLenOrInd*) ，其位址會傳遞給 **SQLGetData** ，因為對應的資料緩衝區 (*ValuePtr*) 是 nondeferred 輸出緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非明確禁止，否則長度/指標緩衝區引數可以是 0 (如果 nondeferred 輸入) ，或如果輸出或延遲輸入) ，則為 null 指標 (。 針對輸入緩衝區，這會導致驅動程式忽略資料的位元組長度。 當傳遞可變長度的資料時，這會傳回錯誤，但在傳遞非 null、固定長度的資料時很常見，因為長度和指標值都不需要。 針對輸出緩衝區，這會導致驅動程式不傳回資料的位元組長度或指標值。 如果驅動程式所傳回的資料是 Null，但在抓取固定長度的不可為 null 的資料時很常見，因為長度和指標值都不需要。  
  
 當延遲資料緩衝區的位址傳遞至驅動程式時，延後長度/指標緩衝區的位址必須維持有效，直到緩衝區解除系結為止。  
  
 下列長度是有效的長度/指標值：  
  
-   *n*，其中 *n* > 0。  
  
-   0.  
  
-   SQL_NTS。 在對應的資料緩衝區中傳送至驅動程式的字串是以 null 結束;這是 C 程式設計人員在不需要計算位元組長度的情況下傳遞字串的便利方式。 只有當應用程式將資料傳送至驅動程式時，此值才是合法的。 當驅動程式將資料傳回到應用程式時，它一律會傳回實際的資料位元組長度。  
  
 下列值是有效的長度/指標值。 SQL_Null_DATA 儲存在 SQL_DESC_INDICATOR_PTR 描述項欄位中;所有其他值都會儲存在 SQL_DESC_OCTET_LENGTH_PTR 描述項欄位中。  
  
-   SQL_Null_DATA。 資料是 Null 資料值，而對應資料緩衝區中的值會被忽略。 此值僅適用于從驅動程式傳送至或取出的 SQL 資料。  
  
-   SQL_DATA_AT_EXEC。 資料緩衝區不包含任何資料。 相反地，當執行語句或呼叫**SQLBulkOperations**或**SQLSetPos**時，資料會以**SQLPutData**傳送。 此值僅適用于傳送至驅動程式的 SQL 資料。 如需詳細資訊，請參閱 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)和 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   SQL_LEN_DATA_AT_EXEC (*長度*) 宏的結果。 此值類似于 SQL_DATA_AT_EXEC。 如需詳細資訊，請參閱傳送 [長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驅動程式無法判斷在輸出緩衝區中仍可傳回的長資料位元組數。 此值僅適用于從驅動程式取出的 SQL 資料。  
  
-   SQL_DEFAULT_PARAM。 程式是在程式中使用輸入參數的預設值，而不是對應資料緩衝區中的值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulkOperations** 或 **SQLSetPos** 會忽略資料緩衝區中的值。 藉由呼叫 **SQLBulkOperations** 或 SQLSetPos 來更新資料列時 **，** 資料行值不會變更。 當您呼叫 **SQLBulkOperations**來插入新的資料列時，資料行值會設定為其預設值，如果資料行沒有預設值，則會設為 Null。
