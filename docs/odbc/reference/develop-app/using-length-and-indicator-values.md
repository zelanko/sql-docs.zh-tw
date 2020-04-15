---
title: 使用長度和指標值 |微軟文件
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
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306759"
---
# <a name="using-length-and-indicator-values"></a>使用長度與指標值
長度/指示器緩衝區用於傳遞數據緩衝區中數據的位元組長度或特殊指標(如SQL_NULL_DATA,指示數據為 NULL。 根據使用它的函數,長度/指示器緩衝區定義為 SQLINTEGER 或 SQLSMALLINT。 因此,需要單個參數來描述它。 如果數據緩衝區是非延遲輸入緩衝區,則此參數包含數據本身的位元組長度或指標值。 它通常命名為*StrLen_or_Ind*或類似的名稱。 例如,以下代碼調用**SQLPutData**來傳遞充滿數據的緩衝區;位元組長度 (*ValueLen*) 直接傳遞,因為數據緩衝區 (*ValuePtr*) 是輸入緩衝區。  
  
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
  
 如果數據緩衝區是延遲輸入緩衝區、非延遲輸出緩衝區或輸出緩衝區,則參數包含長度/指示器緩衝區的位址。 它通常命名為*StrLen_or_IndPtr*或類似的名稱。 例如,以下代碼調用**SQLGetData**來檢索充滿數據的緩衝區;位元組長度傳回到長度/指標緩衝區 *(ValueLenOrInd)* 中的應用程式,其位址傳遞給**SQLGetData,** 因為相應的數據緩衝區 *(ValuePtr*) 是非延遲輸出緩衝區。  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 除非特別禁止,否則長度/指示器緩衝區參數可以是 0(如果未延遲輸入)或空指標(如果輸出或延遲輸入)。 對於輸入緩衝區,這將導致驅動程式忽略數據的位元組長度。 這在傳遞可變長度數據時返回錯誤,但在傳遞非空固定長度數據時很常見,因為不需要長度或指標值。 對於輸出緩衝區,這將導致驅動程式不返回數據的位元組長度或指標值。 如果驅動程式返回的數據為 NULL,但在檢索固定長度的非空數據時很常見,則這是一個錯誤,因為不需要長度和指標值。  
  
 當延遲數據緩衝區的位址傳遞給驅動程式時,延遲長度/指示器緩衝區的位址必須保持有效,直到緩衝區未綁定。  
  
 以下長度作為長度/指示器值有效:  
  
-   *n*,*其中 n* > 0。  
  
-   0.  
  
-   SQL_NTS 發送到相應資料緩衝區中的驅動程式的字串為 null 終止;因此,發送到驅動程式的字串為 null,為"已終止」。這是 C 程式師傳遞字串而無需計算位元組長度的便捷方法。 僅當應用程式將數據發送到驅動程式時,此值才是合法的。 當驅動程式將數據返回給應用程式時,它始終返回數據的實際位元組長度。  
  
 以下值作為長度/指示器值有效。 SQL_NULL_DATA存儲在SQL_DESC_INDICATOR_PTR描述符欄位中;所有其他值都存儲在SQL_DESC_OCTET_LENGTH_PTR描述符欄位中。  
  
-   SQL_NULL_DATA 資料是 NULL 資料值,並忽略相應數據緩衝區中的值。 此值僅適用於發送到驅動程式或從驅動程式檢索的 SQL 資料。  
  
-   SQL_DATA_AT_EXEC 數據緩衝區不包含任何數據。 相反,當執行語句或調用**SQLBulk 操作**或**SQLSetPos**時,數據將隨**SQLPutData**一起發送。 此值僅適用於發送到驅動程式的 SQL 資料。 有關詳細資訊,請參閱[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md) [、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)與[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
-   SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果。 此值類似於SQL_DATA_AT_EXEC。 有關詳細資訊,請參閱[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
-   SQL_NO_TOTAL。 驅動程式無法確定仍可在輸出緩衝區中返回的長數據位元組數。 此值僅適用於從驅動程式檢索的 SQL 資料。  
  
-   SQL_DEFAULT_PARAM 過程是在過程中使用輸入參數的預設值,而不是相應數據緩衝區中的值。  
  
-   SQL_COLUMN_IGNORE。 **SQLBulk 操作**或**SQLSetPos**是忽略數據緩衝區中的值。 通過調用**SQLBulk 操作**或**SQLSetPos**更新一行數據時,列值不會更改。 當透過調用**SQLBulk 操作**插入新資料列時,列值將設置為其預設值,或者如果列沒有預設值,則設置為 NULL。
