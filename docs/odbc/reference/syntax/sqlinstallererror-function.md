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
manager: craigg
ms.openlocfilehash: a0ae475ba4dc290f57eadf94d1e45e8a203a7ce5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536601"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLInstallerError**傳回 ODBC 安裝程式函式的錯誤或狀態資訊。  
  
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
 [輸入]錯誤記錄號碼。 有效的數字是從 1 到 8。  
  
 *pfErrorCode*  
 [輸出]安裝程式錯誤碼。 （如需詳細資訊，請參閱 「 註解。"）  
  
 *lpszErrorMsg*  
 [輸出]錯誤訊息文字的儲存體的指標。  
  
 *cbErrorMsgMax*  
 [輸入]最大長度*szErrorMsg*緩衝區。 這必須是小於或等於 SQL_MAX_MESSAGE_LENGTH 減去之 null 結束字元。  
  
 *cbErrorMsgMax*  
 [輸入]最大長度*szErrorMsg*緩衝區。 這必須是小於或等於 SQL_MAX_MESSAGE_LENGTH 減去之 null 結束字元。  
  
 *pcbErrorMsg*  
 [輸出]指標的總位元組數 （不包括 null 結束字元） 可用以傳回*lpszErrorMsg*。 如果傳回可用的位元組數目大於或等於*cbErrorMsgMax*中的錯誤訊息文字*lpszErrorMsg*會被截斷成*cbErrorMsgMax*減號null 結束字元位元組。 *PcbErrorMsg*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 sql_no_data 之後或 SQL_ERROR。  
  
## <a name="diagnostics"></a>診斷  
 **SQLInstallerError**本身未公佈錯誤值。 **SQLInstallerError**傳回 sql_no_data 為止，無法擷取任何錯誤訊息時 (在此情況下*pfErrorCode*是未定義)。 如果**SQLInstallerError**無法存取錯誤值通常會傳回 SQL_ERROR，任何原因**SQLInstallerError**會傳回 SQL_ERROR，但不會將任何錯誤的值。 如果您不知道警告字串的長度 (*lpszErrorMsg*)，您可以設定*lpszErrorMsg*為 NULL，而且呼叫**SQLInstallerError**。 **SQLInstallerError**將則會傳回警告中之字串的長度*cbErrorMsgMax*。 如果錯誤訊息的緩衝區太短時， **SQLInstallerError**會傳回 SQL_SUCCESS_WITH_INFO，並傳回正確*pfErrorCode*值**SQLInstallerError**.  
  
 若要判斷錯誤訊息中是否發生截斷，應用程式可以比較中的值*cbErrorMsgMax*要寫入的訊息文字的實際長度的引數*pcbErrorMsg*引數。 如果確實發生截斷，正確的緩衝區長度應配置給*lpszErrorMsg*並**SQLInstallerError**應該會再次呼叫具有對應*Irc*記錄。  
  
## <a name="comments"></a>註解  
 應用程式呼叫**SQLInstallerError**當上一個呼叫 ODBC 安裝程式函式會傳回 FALSE。 ODBC 安裝程式和驅動程式或轉譯器設定的函式後的零個或多個錯誤，函式失敗時，才 （會傳回 FALSE）;因此，應用程式呼叫**SQLInstallerError**只 ODBC 安裝程式函式會在失敗之後。  
  
 ODBC 安裝程式錯誤佇列會排清每次呼叫新的安裝程式函式時。 因此，不能期望應用程式，來擷取最後一個安裝程式函式呼叫的函式以外的錯誤。  
  
 若要擷取的函式呼叫的多個錯誤，應用程式會呼叫**SQLInstallerError**多次。  
  
 當沒有其他的資訊**SQLInstallerError**傳回 sql_no_data 為止， *pfErrorCode*引數是未定義， *pcbErrorMsg*引數等於 0，及*lpszErrorMsg*引數包含 null 結束的單一字元 (除非*cbErrorMsgMax*引數等於 0)。
