---
title: SQLGetDiarec 函數 |微軟文件
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
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285378"
---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetDiagRec**傳回包含錯誤、警告和狀態資訊的診斷記錄多個字段的當前值。 與**SQLGetDiagField**(每次呼叫返回一個診斷欄位 ) 不同 **,SQLGetDiagRec**返回診斷記錄的幾個常用欄位,包括 SQLSTATE、本機錯誤代碼和診斷消息文本。  
  
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
 [輸入]描述需要診斷的句柄類型的句柄類型標識符。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN句柄僅由驅動程式管理器和驅動程式使用。 應用程式不應使用此句柄類型。 有關SQL_HANDLE_DBC_INFO_TOKEN的詳細資訊,請參閱在[ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]診斷數據結構的句柄,由*HandleType*指示的類型。 如果*HandleType*是SQL_HANDLE_ENV,*則句柄*可以是共用環境句柄,也可以是非共用環境句柄。  
  
 *RecNumber*  
 [輸入]指示應用程式從中查找資訊的狀態記錄。 狀態記錄從 1 編號。  
  
 *SQLState*  
 【輸出]指向用於返回診斷記錄*RecNumber*的五個字元 SQLSTATE 代碼(和終止 NULL)的緩衝區的指標。 前兩個字元指示類;第二個字元指示類。接下來的三個表示子類。 此資訊包含在SQL_DIAG_SQLSTATE診斷欄位中。 有關詳細資訊,請參閱[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。  
  
 *這個機錯誤 Ptr*  
 【輸出]指向緩衝區的指標,用於返回特定於數據源的本機錯誤代碼。 此資訊包含在SQL_DIAG_NATIVE診斷欄位中。  
  
 *MessageText*  
 【輸出]指向要返回診斷消息文本字串的緩衝區的指標。 此資訊包含在SQL_DIAG_MESSAGE_TEXT診斷欄位中。 有關字串的格式,請參閱[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。  
  
 如果*MessageText*為*NULL,TextLengthPtr*仍將傳回可在*MessageText*指向的緩衝區中返回的字元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]以字元表示*消息文本*緩衝區的長度。 診斷消息文本沒有最大長度。  
  
 *文字長度 Ptr*  
 【輸出]指向一個緩衝區的指標,其中返回可在*\*MessageText*中傳回的字元總數(不包括 null 終止字元所需的字元數)。 如果可用傳回的字元數大於*BufferLength,* 則*\*MessageText*中的診斷訊息文本將截斷為*BufferLength*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagRec**不會自行發佈診斷記錄。 它使用以下返回值來報告其自身執行的結果:  
  
-   SQL_SUCCESS:該功能已成功返回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO:\**消息文本*緩衝區太小,無法保存請求的診斷消息。 未生成診斷記錄。 要確定發生截斷,應用程式必須將*BufferLength*與實際可用位元組數進行比較,該位元組數寫入 **StringLengthPtr*。  
  
-   *SQL_INVALID_HANDLE:HandleType*和*Handle*指示的句柄不是有效的句柄。  
  
-   SQL_ERROR: 發生了以下情況之一:  
  
    -   *RecNumber*為負數或 0。  
  
    -   *緩衝區長度*小於零。  
  
    -   使用非同步通知時,句柄上的非同步操作未完成。  
  
-   SQL_NO_DATA: *RecNumber*大於*在 Handle*中指定的句柄存在的診斷記錄數。 如果*Handle*沒有診斷記錄,則函數還會返回任何正*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>註解  
 當以前對 ODBC 函數的調用已返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,應用程式通常調用**SQLGetDiagRec。** 但是,由於任何 ODBC 函數每次調用時都可以發佈零個或多個診斷記錄,因此應用程式可以在任何 ODBC 函數調用後調用**SQLGetDiarec。** 應用程式可以多次調用**SQLGetDiagRec**以返回診斷數據結構中的部分或全部記錄。 ODBC 對可同時存儲的診斷記錄的數量沒有限制。  
  
 **SQLGetDiagRec**不能用於從診斷數據結構的標頭返回欄位。 *(RecNumber*參數必須大於 0。為此,應用程式應調用**SQLGetDiagField。**  
  
 **SQLGetDiagRec**僅檢索最近與*Handle*參數中指定的句柄關聯的診斷資訊。 如果應用程式呼叫另一個 ODBC 函數 **(SQLGetDiarec、SQLGetDiagField**或**SQLError),** 則同一句柄上以前調用的**SQLGetDiagField**任何診斷資訊都丟失。  
  
 應用程式可以通過迴圈掃描所有診斷記錄,增加*RecNumber,* 只要**SQLGetDiagRec**返回SQL_SUCCESS。 對**SQLGetDiagRec 的**調用對標頭和記錄欄位沒有破壞性。 應用程式可以在以後再次調用**SQLGetDiagRec**從記錄中檢索欄位,只要在此期間沒有調用除**SQLGetDiagRec、SQLGetDiagField****SQLGetDiagField**或**SQLError**之外的其他函數。 應用程式還可以檢索可用診斷記錄總數計數,通過調用**SQLGetDiagField**檢索SQL_DIAG_NUMBER欄位的值,然後多次調用**SQLGetDiagRec。**  
  
 有關診斷資料結構欄位的說明,請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。 有關詳細資訊,請參閱使用[SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) [並實現 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 調用非同步執行的 API 以外的 API 將生成 HY010"函數序列錯誤" 但是,在異步操作完成之前無法檢索錯誤記錄。  
  
## <a name="handletype-argument"></a>句柄類型參數  
 每個句柄類型都可以具有與其關聯的診斷資訊。 *HandleType*參數表示*句柄*參數的句柄類型。  
  
 無法為環境、連接、語句和描述符句柄返回某些標頭和記錄欄位。 在[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的「標題欄位」和「記錄欄位」部分中指示欄位不適用的句柄。  
  
 如果*handleType*是SQL_HANDLE_SENV的,則對**SQLGetDiagRec**的調用將返回SQL_INVALID_HANDLE,該操作表示共用環境句柄。 但是,如果*HandleType* SQL_HANDLE_ENV,*則句柄*可以是共用環境句柄,也可以是非共用環境句柄。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷記錄的欄位或診斷標頭的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
