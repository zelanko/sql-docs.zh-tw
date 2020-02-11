---
title: SQLGetDiagRec 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c404cbb1f29adbdcb49ef6bed8bb57a047f64f3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911323"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函式
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**會傳回診斷記錄中多個欄位的目前值，其中包含錯誤、警告和狀態資訊。 不同于**SQLGetDiagField**會針對每個呼叫傳回一個診斷欄位， **SQLGetDiagRec**會傳回診斷記錄的數個常用欄位，包括 SQLSTATE、原生錯誤碼和診斷郵件內文。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源控制碼類型識別碼，描述需要診斷的控制碼類型。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼僅供驅動程式管理員和驅動程式使用。 應用程式不應使用此控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *圖*  
 源*HandleType*所指示之類型的診斷資料結構的控制碼。 如果*HandleType*為 SQL_HANDLE_ENV，則*handle*可以是共用或非共用的環境控制碼。  
  
 *RecNumber*  
 源表示應用程式用來搜尋資訊的狀態記錄。 狀態記錄的編號為1。  
  
 *SQLState*  
 輸出緩衝區的指標，在其中傳回診斷記錄*RecNumber*的五個字元的 SQLSTATE 碼（和終止 Null）。 前兩個字元表示類別;接下來的三個指示子類別。 這項資訊包含在 [SQL_DIAG_SQLSTATE 診斷] 欄位中。 如需詳細資訊，請參閱[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 輸出緩衝區的指標，要在其中傳回原生錯誤碼（特定于資料來源）。 這項資訊包含在 [SQL_DIAG_NATIVE 診斷] 欄位中。  
  
 *MessageText*  
 輸出要在其中傳回診斷消息文字字串之緩衝區的指標。 這項資訊包含在 [SQL_DIAG_MESSAGE_TEXT 診斷] 欄位中。 如需字串的格式，請參閱[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*為 Null， *TextLengthPtr*仍會傳回*MessageText*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源**MessageText*緩衝區的長度（以字元為單位）。 診斷郵件內文沒有最大長度。  
  
 *TextLengthPtr*  
 輸出緩衝區的指標，要在其中傳回* \*MessageText*中可傳回的字元總數（不包括 null 終止字元所需的字元數）。 如果可傳回的字元數大於*BufferLength*， * \*MessageText*中的診斷郵件內文會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagRec**不會為其本身張貼診斷記錄。 它會使用下列傳回值來報告其本身執行的結果：  
  
-   SQL_SUCCESS：函數已成功傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO： \* *MessageText*緩衝區太小，無法保存所要求的診斷訊息。 未產生任何診斷記錄。 若要判斷是否發生截斷，應用程式必須將*BufferLength*與實際可用的位元組數目（寫入 **StringLengthPtr*）進行比較。  
  
-   SQL_INVALID_HANDLE： *HandleType*和*HANDLE*所指示的控制碼不是有效的控制碼。  
  
-   SQL_ERROR：發生下列其中一種情況：  
  
    -   *RecNumber*為負數或0。  
  
    -   *BufferLength*小於零。  
  
    -   使用非同步通知時，控制碼上的非同步作業並未完成。  
  
-   SQL_NO_DATA： *RecNumber*大於 handle 中指定之控制碼所存在的診斷記錄數目 *。* 如果沒有任何適用于*Handle*的診斷記錄，函數也會傳回任何正面*RecNumber*的 SQL_NO_DATA。  
  
## <a name="comments"></a>註解  
 應用程式通常會在上一次呼叫 ODBC 函式傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時呼叫**SQLGetDiagRec** 。 不過，由於任何 ODBC 函數每次呼叫時都可以張貼零或多個診斷記錄，因此應用程式可以在任何 ODBC 函數呼叫之後呼叫**SQLGetDiagRec** 。 應用程式可以多次呼叫**SQLGetDiagRec** ，以傳回診斷資料結構中的部分或全部記錄。 ODBC 不會限制任何一次可以儲存的診斷記錄數目。  
  
 **SQLGetDiagRec**不能用來從診斷資料結構的標頭傳回欄位。 （ *RecNumber*引數必須大於0。）基於此目的，應用程式應該呼叫**SQLGetDiagField** 。  
  
 **SQLGetDiagRec**只會抓取最近與*handle*引數中指定之控制碼相關聯的診斷資訊。 如果應用程式呼叫另一個 ODBC 函數（ **SQLGetDiagRec**、 **SQLGetDiagField**或**SQLError**除外），則會遺失來自相同控制碼上先前呼叫的任何診斷資訊。  
  
 只要**SQLGetDiagRec**傳回 SQL_SUCCESS，應用程式就可以藉由迴圈、遞增*RecNumber*來掃描所有診斷記錄。 對**SQLGetDiagRec**的呼叫在標頭和記錄欄位中是非破壞性的。 只要沒有其他函式（ **SQLGetDiagRec**、 **SQLGetDiagField**或**SQLError**除外）已在過渡期呼叫，應用程式就可以在稍後再次呼叫**SQLGetDiagRec** ，以從記錄中取出欄位。 應用程式也可以藉由呼叫**SQLGetDiagField**來抓取 [SQL_DIAG_NUMBER] 欄位的值，然後多次呼叫**SQLGetDiagRec** ，藉此抓取診斷記錄總數的計數。  
  
 如需診斷資料結構之欄位的說明，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 如需詳細資訊，請參閱[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[執行 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不是以非同步方式執行的 API，將會產生 HY010 「函數順序錯誤」。 不過，在非同步作業完成之前，無法抓取錯誤記錄。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制碼類型都可以有相關聯的診斷資訊。 *HandleType*引數代表*控制碼*引數的控制碼類型。  
  
 某些標頭和記錄欄位無法針對環境、連接、語句和描述項控制碼傳回。 欄位不適用的控制碼會顯示在[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的「標頭欄位」和「記錄欄位」區段中。  
  
 如果*HandleType*是 SQL_HANDLE_SENV （代表共用的環境控制碼），則呼叫**SQLGetDiagRec**會傳回 SQL_INVALID_HANDLE。 不過，如果*HandleType*是 SQL_HANDLE_ENV，則*HANDLE*可以是共用或非共用的環境控制碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷記錄的欄位或診斷標頭的欄位|[SQLGetDiagField 函數](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
