---
description: SQLGetDiagRec 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7f141891292fb80d53ba06e03329b66cbc8b826e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461011"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetDiagRec** 會傳回診斷記錄的多個欄位目前的值，其中包含錯誤、警告和狀態資訊。 不同于 **SQLGetDiagField**（每次呼叫會傳回一個診斷欄位）， **SQLGetDiagRec** 會傳回診斷記錄的數個常用欄位，包括 SQLSTATE、原生錯誤碼，以及診斷郵件內文。  
  
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
 輸出控制碼類型識別碼，描述需要診斷的控制碼類型。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼只能由驅動程式管理員和驅動程式使用。 應用程式不應該使用這個控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 輸出診斷資料結構的控制碼， *HandleType*所指出的型別。 如果 *HandleType* 是 SQL_HANDLE_ENV， *控制碼* 可以是共用或非共用的環境控制碼。  
  
 *RecNumber*  
 輸出指出應用程式用來搜尋資訊的狀態記錄。 狀態記錄是從1開始編號。  
  
 *SQLState*  
 出緩衝區的指標，此緩衝區會傳回五個字元的 SQLSTATE 程式碼 (以及終止診斷記錄 *RecNumber*的 Null) 。 前兩個字元表示類別：接下來的三個表示子類別。 這項資訊包含在 SQL_DIAG_SQLSTATE 診斷] 欄位中。 如需詳細資訊，請參閱 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 出要傳回原生錯誤碼的緩衝區指標，特定于資料來源。 這項資訊包含在 SQL_DIAG_NATIVE 診斷] 欄位中。  
  
 *MessageText*  
 出要傳回診斷郵件內文字串的緩衝區指標。 這項資訊包含在 SQL_DIAG_MESSAGE_TEXT 診斷] 欄位中。 如需字串的格式，請參閱 [診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果 *MessageText* 是 Null， *TextLengthPtr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *MessageText*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出**MessageText* 緩衝區的長度（以字元為單位）。 診斷郵件內文沒有最大長度。  
  
 *TextLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回字元總數 (不包括 null 終止字元所需的字元數) 可在* \* MessageText*中傳回。 如果可傳回的字元數大於*BufferLength*， * \* MessageText*中的診斷郵件內文會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagRec** 不會張貼本身的診斷記錄。 它會使用下列傳回值來報告本身執行的結果：  
  
-   SQL_SUCCESS：函式已成功傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO： \* *MessageText*緩衝區太小，無法保存要求的診斷訊息。 未產生任何診斷記錄。 若要判斷是否發生截斷，應用程式必須將 *BufferLength* 與可用的實際位元組數目（寫入 **StringLengthPtr*）進行比較。  
  
-   SQL_INVALID_HANDLE： *HandleType* 和 *Handle* 所指出的控制碼不是有效的控制碼。  
  
-   SQL_ERROR：發生下列其中一種情況：  
  
    -   *RecNumber* 為負數或0。  
  
    -   *BufferLength* 小於零。  
  
    -   使用非同步通知時，控制碼上的非同步作業未完成。  
  
-   SQL_NO_DATA： *RecNumber*大於*控制碼*中指定之控制碼所存在的診斷記錄數目。 如果沒有任何用於*處理*的診斷記錄，此函數也會傳回任何正面*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>註解  
 當先前對 ODBC 函數的呼叫傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，應用程式通常會呼叫 **SQLGetDiagRec** 。 不過，因為任何 ODBC 函數每次呼叫時都可以張貼零或多個診斷記錄，所以應用程式可以在任何 ODBC 函式呼叫之後呼叫 **SQLGetDiagRec** 。 應用程式可以多次呼叫 **SQLGetDiagRec** ，以傳回診斷資料結構中的部分或所有記錄。 ODBC 對可隨時儲存的診斷記錄數目沒有任何限制。  
  
 **SQLGetDiagRec** 不能用來從診斷資料結構的標頭傳回欄位。  (*RecNumber* 引數必須大於0。 ) 應用程式應該針對此目的呼叫 **SQLGetDiagField** 。  
  
 **SQLGetDiagRec** 只會抓取最近與 *控制碼* 引數中指定之控制碼相關聯的診斷資訊。 如果應用程式呼叫另一個 ODBC 函數，但 **SQLGetDiagRec**、 **SQLGetDiagField**或 **SQLError**例外，則相同控制碼上先前呼叫的任何診斷資訊都會遺失。  
  
 只要**SQLGetDiagRec**傳回 SQL_SUCCESS，應用程式就可以藉由迴圈、遞增*RecNumber*來掃描所有診斷記錄。 對 **SQLGetDiagRec** 的呼叫不會與標頭和記錄欄位有破壞性。 只要在過渡期間呼叫了**SQLGetDiagRec**、 **SQLGetDiagField**或**SQLError**以外的其他函式，應用程式稍後可以再次呼叫**SQLGetDiagRec** ，以從記錄中取出欄位。 應用程式也可以藉由呼叫 **SQLGetDiagField** 來取出 SQL_DIAG_NUMBER 欄位的值，然後呼叫 **SQLGetDiagRec** 多次，來取得可用診斷記錄總數的計數。  
  
 如需診斷資料結構之欄位的說明，請參閱 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 如需詳細資訊，請參閱 [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 和 [執行 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫非以非同步方式執行的 API 將會產生 HY010 「函式順序錯誤」。 但是，在非同步作業完成之前，無法抓取錯誤記錄。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制碼類型都可以有相關聯的診斷資訊。 *HandleType*引數代表*控制碼*引數的控制碼類型。  
  
 某些標頭和記錄欄位無法針對環境、連接、語句和描述項控制碼傳回。 欄位未適用的控制碼會顯示在 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)的 [標頭欄位] 和 [記錄欄位] 區段中。  
  
 如果*HandleType*是 SQL_HANDLE_SENV （代表共用的環境控制碼），呼叫**SQLGetDiagRec**將會傳回 SQL_INVALID_HANDLE。 但是，如果 *HandleType* 是 SQL_HANDLE_ENV， *控制碼* 可以是共用或非共用的環境控制碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷記錄的欄位或診斷標頭的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
