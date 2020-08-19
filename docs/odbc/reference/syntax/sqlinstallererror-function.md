---
description: SQLInstallerError 函式
title: SQLInstallerError 函式 |Microsoft Docs
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
ms.openlocfilehash: fcc5f89a40802e6efa405771474cda3e86f4519c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421162"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLInstallerError** 會傳回 ODBC 安裝程式函數的錯誤或狀態資訊。  
  
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
 *iError*  
 輸出錯誤記錄號碼。 有效的數位是從1到8。  
  
 *pfErrorCode*  
 出安裝程式錯誤碼。  (需詳細資訊，請參閱「批註」。)   
  
 *lpszErrorMsg*  
 出錯誤訊息正文的儲存指標。  
  
 *cbErrorMsgMax*  
 輸出 *SzErrorMsg* 緩衝區的最大長度。 這必須小於或等於 SQL_MAX_MESSAGE_LENGTH 減去 null 終止字元。  
  
 *cbErrorMsgMax*  
 輸出 *SzErrorMsg* 緩衝區的最大長度。 這必須小於或等於 SQL_MAX_MESSAGE_LENGTH 減去 null 終止字元。  
  
 *pcbErrorMsg*  
 出位元組總數的指標 (不包括 null 終止字元) 可在 *lpszErrorMsg*中傳回。 如果可傳回的位元組數目大於或等於 *cbErrorMsgMax*， *lpszErrorMsg* 中的錯誤訊息正文會截斷為 *cbErrorMsgMax* 減去 null 結束字元位元組。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLInstallerError** 不會張貼本身的錯誤值。 當**SQLInstallerError**無法取得任何錯誤資訊時，會傳回 SQL_NO_DATA (在此情況下， *pfErrorCode*未定義) 。 如果 **SQLInstallerError** 因任何通常會傳回 SQL_ERROR 的原因而無法存取錯誤值，則 **SQLInstallerError** 會傳回 SQL_ERROR 但不會張貼任何錯誤值。 如果您不知道警告字串的長度 (*lpszErrorMsg*) ，您可以將 *LPSZERRORMSG* 設定為 Null，然後呼叫 **SQLInstallerError**。 然後， **SQLInstallerError**會傳回*cbErrorMsgMax*中警告字串的長度。 如果錯誤訊息的緩衝區太短， **SQLInstallerError**會傳回 SQL_SUCCESS_WITH_INFO，並傳回**SQLInstallerError**的正確*pfErrorCode*值。  
  
 若要判斷錯誤訊息中是否發生截斷，應用程式可以比較 *cbErrorMsgMax* 引數中的值與寫入 *pcbErrorMsg* 引數之郵件內文的實際長度。 如果發生截斷，則應該為*lpszErrorMsg*配置正確的緩衝區長度，並使用對應的*iError*記錄再次呼叫**SQLInstallerError** 。  
  
## <a name="comments"></a>註解  
 當先前對 ODBC 安裝程式函數的呼叫傳回 FALSE 時，應用程式會呼叫 **SQLInstallerError** 。 只有當函式失敗時，ODBC 安裝程式和驅動程式或翻譯工具安裝函式才會張貼零或多個錯誤 (傳回 FALSE) ;因此，只有在 ODBC 安裝程式函數失敗之後，應用程式才會呼叫 **SQLInstallerError** 。  
  
 每次呼叫新的安裝程式函數時，就會清除 ODBC 安裝程式錯誤佇列。 因此，應用程式不會預期從最後一個安裝程式函式呼叫取得其他函式的錯誤。  
  
 為了取得函式呼叫的多個錯誤，應用程式會呼叫 **SQLInstallerError** 多次。  
  
 當沒有其他資訊時， **SQLInstallerError** 會傳回 SQL_NO_DATA、 *pfErrorCode* 引數為未定義、 *pcbErrorMsg* 引數等於0，而且 *lpszErrorMsg* 引數包含單一 null 終止字元 (除非 *cbErrorMsgMax* 引數等於 0) 。
