---
title: "SQLGetDiagRec 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 591664f329f4c7feeb24fff52b809dba567d0b80
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**傳回多個欄位包含錯誤、 警告和狀態資訊的診斷記錄的目前值。 不同於**SQLGetDiagField**，它會傳回一個診斷欄位，每個呼叫， **SQLGetDiagRec**數個常用的診斷記錄，包括 SQLSTATE、 自發性錯誤程式碼中，欄位會傳回與診斷訊息文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]描述診斷所需的控制代碼的類型控制代碼類型識別項。 必須是下列其中之一：  
  
-   利用 SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   利用 SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應該使用此控制代碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]如需診斷資料結構，所指定的類型的控制代碼*HandleType*。 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或共用的環境控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的狀態記錄。 狀態記錄編號 1。  
  
 *SQLState*  
 [輸出]要傳回五個字元的 SQLSTATE 程式碼 （和結束的 NULL），以供診斷記錄的緩衝區指標*RecNumber*。 前兩個字元表示類別; 事件類別下一步的三個表示子類別。 這項資訊包含在 SQL_DIAG_SQLSTATE 診斷欄位。 如需詳細資訊，請參閱[Sqlstate](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 [輸出]這是要傳回的原生錯誤碼，資料來源特定的緩衝區指標。 這項資訊包含在 SQL_DIAG_NATIVE 診斷欄位。  
  
 *MessageText*  
 [輸出]這是要傳回的診斷訊息的文字字串的緩衝區指標。 這項資訊包含在 SQL_DIAG_MESSAGE_TEXT 診斷欄位。 字串的格式，請參閱[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*是 NULL， *TextLengthPtr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*MessageText*。  
  
 *Columnsize*  
 [輸入]長度 **MessageText*以字元為單位的緩衝區。 沒有診斷訊息文字的最大長度。  
  
 *TextLengthPtr*  
 [輸出]這是要傳回的總字元數 （不包括所需的 null 結束字元的字元數） 的緩衝區指標可用來傳回中* \*MessageText*。 如果要傳回的字元數目大於*Columnsize*中的診斷訊息文字* \*MessageText*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagRec**不會將其本身的診斷記錄。 它會使用下列傳回值報告自己執行的結果：  
  
-   SQL_SUCCESS： 函式成功地傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO: \* *MessageText*緩衝區太小，無法保留要求的診斷訊息。 未不產生任何診斷記錄。 若要判定發生截斷，應用程式必須比較*Columnsize*實際可用的位元組數目，這會寫入至 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE： 所指定的控制代碼*HandleType*和*處理*不是有效的控制代碼。  
  
-   SQL_ERROR： 下列其中一項發生：  
  
    -   *RecNumber*是負數或 0。  
  
    -   *Columnsize*小於零。  
  
    -   當使用非同步通知時，控制代碼的非同步作業未完成。  
  
-   SQL_NO_DATA: *RecNumber*診斷記錄中指定的控制代碼已存在的數目大於*處理。* 函式也會傳回 SQL_NO_DATA 任何正值*RecNumber*是否有任何的診斷記錄*處理*。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLGetDiagRec**當先前呼叫 ODBC 函數傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 不過，因為任何 ODBC 函數可以張貼零或多個診斷記錄每次呼叫時，應用程式可以呼叫**SQLGetDiagRec**之後的任何 ODBC 函數呼叫。 應用程式可以呼叫**SQLGetDiagRec**多次，以便傳回診斷資料結構中的部分或所有的記錄。 ODBC 會加諸一次可以儲存的診斷記錄的數目沒有限制。  
  
 **SQLGetDiagRec**無法用來傳回診斷資料結構中的標頭中的欄位。 ( *RecNumber*引數必須是大於 0。)應用程式應該呼叫**SQLGetDiagField**針對此目的。  
  
 **SQLGetDiagRec**只擷取的診斷資訊最近在指定的控制代碼相關聯*處理*引數。 如果應用程式呼叫另一個 ODBC 函式，除非**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，從先前的呼叫上的任何診斷資訊相同的控制代碼將會遺失。  
  
 應用程式可以掃描所有的診斷記錄迴圈、 遞增*RecNumber*，只要**SQLGetDiagRec**都會傳回 SQL_SUCCESS。 呼叫**SQLGetDiagRec**會恢復至標頭和記錄欄位。 應用程式可以呼叫**SQLGetDiagRec**再次在稍後擷取的欄位從一筆記錄，只要為沒有其他函式，除了**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，已在過渡期間呼叫。 應用程式也可以藉由呼叫擷取可用的診斷記錄的總數的計數**SQLGetDiagField**來擷取值 SQL_DIAG_NUMBER 欄位，然後呼叫**SQLGetDiagRec**相同次數。  
  
 如需診斷資料結構的欄位的說明，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 如需詳細資訊，請參閱[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不同的非同步執行的應用程式開發介面，將會產生 HY010 「 函數順序錯誤 」。 不過，在非同步作業完成之前，無法擷取記錄時發生錯誤。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制代碼類型可以有與其相關聯的診斷資訊。 *HandleType*引數代表控制代碼類型*處理*引數。  
  
 某些標頭和記錄欄位無法傳回的環境、 連接、 陳述式，以及描述項控制代碼。 中的 「 標頭欄位 」 和 「 記錄欄位 」 章節中所指出的這些控制代碼不適用欄位[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
 呼叫**SQLGetDiagRec**則會傳回 SQL_INVALID_HANDLE *HandleType*是 SQL_HANDLE_SENV，代表共用的環境控制代碼。 不過，如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或共用的環境控制代碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得診斷記錄的欄位或診斷的標頭中的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)

