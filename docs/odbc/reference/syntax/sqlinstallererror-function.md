---
title: SQL安裝程式錯誤功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302099"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQL安裝程式錯誤**傳回 ODBC 安裝程式功能的錯誤或狀態資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引數  
 *i 錯誤*  
 [輸入]錯誤記錄編號。 有效號碼為 1 到 8。  
  
 *pfError 碼*  
 【輸出]安裝程式錯誤代碼。 (有關詳細資訊,請參閱"註釋"。  
  
 *lpsz錯誤Msg*  
 【輸出]指向錯誤消息文本的存儲的指標。  
  
 *cbErrorMsgMax*  
 [輸入]*szErrorMsg*緩衝區的最大長度。 這必須小於或等於SQL_MAX_MESSAGE_LENGTH減去 null 終止字元。  
  
 *cbErrorMsgMax*  
 [輸入]*szErrorMsg*緩衝區的最大長度。 這必須小於或等於SQL_MAX_MESSAGE_LENGTH減去 null 終止字元。  
  
 *多加錯姆斯格*  
 【輸出]指向可用以*lpszErrorMsg*傳回的位元組總數(不包括空終止字元)的指標。 如果可用於返回的位元組數大於或等於*cbErrorMsgMax,**則 lpszErrorMsg*中的錯誤消息文本將被截斷為*cbErrorMsgMax*減去 null 終止字元位元組。 *pcbErrorMsg*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA或SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQL安裝程式錯誤**不會為自己發佈錯誤值。 **當 SQL 安裝程式錯誤**無法檢索任何錯誤資訊(在這種情況下 *,pfErrorCode*未定義)時,它將返回SQL_NO_DATA。 如果**SQL 安裝程式由於**通常返回SQL_ERROR的任何原因無法存取錯誤值,則**SQL 安裝程式錯誤**將返回SQL_ERROR但不過帳任何錯誤值。 如果您不知道警告字串的長度 *(lpszErrorMsg),* 您可以將*lpszErrorMsg*設定為 NULL 並呼叫**SQL 安裝程式錯誤**。 **SQL安裝程式錯誤**將返回*cbErrorMsgMax*中警告字串的長度。 如果錯誤消息的緩衝區太短 **,SQL安裝程式錯誤**將返回SQL_SUCCESS_WITH_INFO並返回**SQL 安裝程式錯誤**的正確*pfErrorCode*值。  
  
 要確定錯誤訊息中是否發生了截斷,應用程式可以將*cbErrorMsgMax*參數中的值與寫入*pcbErrorMsg*參數的消息文本的實際長度進行比較。 如果確實發生截斷,則應為*lpszErrorMg*分配正確的緩衝區長度,並且應使用相應的*iError*記錄再次呼叫**SQL 安裝程式錯誤**。  
  
## <a name="comments"></a>註解  
 當對 ODBC 安裝程式函數的上一個調用返回 FALSE 時,應用程式呼叫**SQL 安裝程式 Error。** ODBC 安裝程式和驅動程式或轉換器設定函數僅在函數失敗時才出現零個或多個錯誤(返回 FALSE);因此,應用程式僅在 ODBC 安裝程式功能失敗後才調用**SQL 安裝程式 Error。**  
  
 每次調用新的安裝程式函數時,都會刷新 ODBC 安裝程式錯誤佇列。 因此,應用程式不能指望檢索上次安裝程式函數調用以外的函數的錯誤。  
  
 若要檢查函式呼叫的多個錯誤,應用程式多次呼叫**SQL 安裝程式錯誤**。  
  
 當沒有其他資訊時 **,SQLInstallerError**返回*SQL_NO_DATA,pfErrorCode*參數未定義 *,pcbErrorMsg*參數等於*0,lpszErrorMsg*參數包含一個空終止字元(除非*cbErrorMgMax*參數等於 0)。
