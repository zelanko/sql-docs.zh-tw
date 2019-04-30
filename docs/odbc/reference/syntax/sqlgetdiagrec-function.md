---
title: SQLGetDiagRec Function | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ab81694fb0234a896a7e9fd09d338e8db43360eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259329"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**傳回多個欄位包含錯誤、 警告和狀態資訊的診斷記錄的目前值。 不同於**SQLGetDiagField**，它會傳回呼叫，每一個診斷欄位**SQLGetDiagRec**傳回幾個常用的診斷記錄，包括 SQLSTATE、 原生錯誤碼的欄位和診斷訊息的文字。  
  
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
 [輸入]描述診斷所需的控制代碼的型別控制代碼型別識別項。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應使用此控制代碼型別。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]診斷資料結構所表示的類型的控制代碼*HandleType*。 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或取消共用的環境控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的狀態記錄。 狀態記錄編號 1。  
  
 *SQLState*  
 [輸出]在其中傳回的五個字元的 SQLSTATE 程式碼 （和終止 NULL） 的診斷記錄緩衝區的指標*RecNumber*。 前兩個字元表示的類別;下列三個指出子類別。 這項資訊包含在 SQL_DIAG_SQLSTATE 診斷欄位。 如需詳細資訊，請參閱 < [Sqlstate](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *NativeErrorPtr*  
 [輸出]在其中傳回的自發性錯誤程式碼，資料來源的特定緩衝區的指標。 這項資訊包含在 SQL_DIAG_NATIVE 診斷欄位。  
  
 *MessageText*  
 [輸出]在其中傳回的診斷訊息的文字字串緩衝區的指標。 這項資訊包含在 SQL_DIAG_MESSAGE_TEXT 診斷欄位。 如需字串的格式，請參閱[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*為 NULL，就*TextLengthPtr*仍會傳回 （不含字元資料的 null 終止字元） 的字元總數可用來傳回中所指向的緩衝區*MessageText*。  
  
 *BufferLength*  
 [輸入]長度 **MessageText*以字元為單位的緩衝區。 沒有診斷訊息文字的最大長度。  
  
 *TextLengthPtr*  
 [輸出]在其中傳回 （不包括 null 結束字元所需的字元數） 的字元總數緩衝區的指標來傳回在可用 *\*MessageText*。 如果可傳回的字元數大於*Columnsize*中的診斷訊息文字 *\*MessageText*會被截斷成*Columnsize*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagRec**不會將本身的診斷記錄。 它會使用下列傳回值報告自己執行的結果：  
  
-   SQL_SUCCESS:此函式會成功地傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO:\* *MessageText*緩衝區太小無法容納要求的診斷訊息。 所不產生的任何診斷記錄。 若要判斷發生截斷，應用程式必須比較*Columnsize*實際的位元組數目，會寫入至 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE:所表示的控制代碼*HandleType*並*處理*不是有效的控制代碼。  
  
-   SQL_ERROR:發生下列其中一項：  
  
    -   *RecNumber*是負數或 0。  
  
    -   *BufferLength*小於零。  
  
    -   當使用非同步通知時，控制代碼的非同步作業未完成。  
  
-   SQL_NO_DATA 為止：*RecNumber*中指定的控制代碼已存在的診斷記錄的數目大於*處理。* 函式也會傳回 SQL_NO_DATA 任何正*RecNumber*沒有診斷記錄是否*處理*。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLGetDiagRec**先前的 ODBC 函式呼叫時傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO。 不過，因為任何 ODBC 函數可以張貼零或多個診斷記錄每次呼叫時，應用程式可以呼叫**SQLGetDiagRec**之後的任何 ODBC 函數呼叫。 應用程式可以呼叫**SQLGetDiagRec**多次，以便傳回診斷資料結構中的部分或全部的記錄。 ODBC 沒有施加限制可以儲存一次的診斷記錄的數目。  
  
 **SQLGetDiagRec**無法用來傳回診斷資料結構中的標頭中的欄位。 ( *RecNumber*引數必須是大於 0。)應用程式應該呼叫**SQLGetDiagField**針對此目的。  
  
 **SQLGetDiagRec**只擷取的診斷資訊最近中指定的控制代碼相關聯*處理*引數。 如果應用程式呼叫另一個的 ODBC 函式，除非**SQLGetDiagRec**， **SQLGetDiagField**，或**SQLError**，在先前的呼叫中的任何診斷資訊相同的控制代碼將會遺失。  
  
 應用程式可以掃描所有的診斷記錄進行迴圈，遞增*RecNumber*，只要**SQLGetDiagRec**都會傳回 SQL_SUCCESS。 若要呼叫**SQLGetDiagRec**是標頭和記錄欄位。 應用程式可以呼叫**SQLGetDiagRec**再於稍後擷取的記錄，只要為沒有其他函式，除了欄位**SQLGetDiagRec**， **SQLGetDiagField**，或是**SQLError**，在此過渡期間被呼叫。 應用程式也可以藉由呼叫擷取可用的診斷記錄的總數的計數**SQLGetDiagField**若要擷取之值 SQL_DIAG_NUMBER 欄位中，然後呼叫**SQLGetDiagRec**的次數。  
  
 如需診斷資料結構的欄位的說明，請參閱 < [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)並[實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不是以非同步方式執行的 API，將會產生 HY010 「 函數順序錯誤 」。 不過，在非同步作業完成之前，無法擷取記錄時發生錯誤。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制代碼類型可以有與其相關聯的診斷資訊。 *HandleType*引數表示的控制代碼類型*處理*引數。  
  
 某些標頭和資料錄的欄位無法為傳回環境、 連接、 陳述式，以及描述項控制代碼。 中的 「 標頭欄位 」 和 「 記錄欄位 」 章節中所指出的這些控制代碼不適用欄位[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
 呼叫**SQLGetDiagRec**則會傳回 SQL_INVALID_HANDLE *HandleType*是 SQL_HANDLE_SENV，代表共用的環境控制代碼。 不過，如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或取消共用的環境控制代碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得的診斷記錄的欄位或診斷的標頭的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
