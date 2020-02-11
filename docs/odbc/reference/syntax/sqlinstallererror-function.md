---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab9461d87a3df2efc98c38e4c72cee4c247fee7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138031"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLInstallerError**會傳回 ODBC 安裝程式功能的錯誤或狀態資訊。  
  
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
 源錯誤記錄號碼。 有效的數位為1到8。  
  
 *pfErrorCode*  
 輸出安裝程式錯誤碼。 （如需詳細資訊，請參閱「留言」）。  
  
 *lpszErrorMsg*  
 輸出錯誤訊息正文之儲存體的指標。  
  
 *cbErrorMsgMax*  
 源*SzErrorMsg*緩衝區的最大長度。 這必須小於或等於 SQL_MAX_MESSAGE_LENGTH 減去 null 終止字元。  
  
 *cbErrorMsgMax*  
 源*SzErrorMsg*緩衝區的最大長度。 這必須小於或等於 SQL_MAX_MESSAGE_LENGTH 減去 null 終止字元。  
  
 *pcbErrorMsg*  
 輸出可在*lpszErrorMsg*中傳回的位元組總數（不包括 null 終止字元）的指標。 如果可傳回的位元組數目大於或等於*cbErrorMsgMax*， *lpszErrorMsg*中的錯誤訊息正文會截斷為*cbErrorMsgMax*減去 null 終止字元的位元組。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLInstallerError**不會為本身張貼錯誤值。 當**SQLInstallerError**無法抓取任何錯誤資訊時，會傳回 SQL_NO_DATA （在此情況下， *pfErrorCode*是未定義的）。 如果**SQLInstallerError**因為任何通常會傳回 SQL_ERROR 的原因而無法存取錯誤值，則**SQLInstallerError**會傳回 SQL_ERROR 但不會張貼任何錯誤值。 如果您不知道警告字串（*lpszErrorMsg*）的長度，您可以將*LPSZERRORMSG*設定為 Null 並呼叫**SQLInstallerError**。 然後， **SQLInstallerError**會傳回*cbErrorMsgMax*中的警告字串長度。 如果錯誤訊息的緩衝區太短，則**SQLInstallerError**會傳回 SQL_SUCCESS_WITH_INFO，並傳回正確的**SQLInstallerError** *pfErrorCode*值。  
  
 若要判斷錯誤訊息中是否發生截斷，應用程式可以比較*cbErrorMsgMax*引數中的值與寫入*pcbErrorMsg*引數之郵件內文的實際長度。 如果發生截斷，應該為*lpszErrorMsg*配置正確的緩衝區長度，而且應該使用對應的*iError*記錄再次呼叫**SQLInstallerError** 。  
  
## <a name="comments"></a>註解  
 當先前的 ODBC 安裝程式函式呼叫傳回 FALSE 時，應用程式會呼叫**SQLInstallerError** 。 只有當函式失敗時，ODBC 安裝程式和驅動程式或轉譯器安裝程式才會公佈零或多個錯誤（傳回 FALSE）;因此，應用程式只有在 ODBC 安裝程式函式失敗之後，才會呼叫**SQLInstallerError** 。  
  
 每次呼叫新的安裝程式函式時，就會清除 ODBC 安裝程式錯誤佇列。 因此，應用程式無法預期從最後一個安裝程式函式呼叫取得以外函數的錯誤。  
  
 若要取得函式呼叫的多個錯誤，應用程式會多次呼叫**SQLInstallerError** 。  
  
 沒有其他資訊時， **SQLInstallerError**會傳回 SQL_NO_DATA、 *pfErrorCode*引數未定義、 *pcbErrorMsg*引數等於0，而*lpszErrorMsg*引數包含單一 null 終止字元（除非*cbErrorMsgMax*引數等於0）。
