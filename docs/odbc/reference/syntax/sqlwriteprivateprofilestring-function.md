---
title: SQLWritePrivateProfileString 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4b847576e503fbbbb511d2dda8f60675c298681c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039378"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函式
**標準**  
 引進的版本： ODBC 2。0  
  
 **摘要**  
 **SQLWritePrivateProfileString**會將值名稱和資料寫入系統資訊的 Odbc 子機碼。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>引數  
 *lpszSection*  
 源指向以 null 終止的字串，其中包含字串將複製到其中的區段名稱。 如果區段不存在，則會加以建立。 區段的名稱與大小寫無關;字串可以是大寫和小寫字母的任意組合。  
  
 *lpszEntry*  
 源指向以 null 終止的字串，其中包含要與字串相關聯的索引鍵名稱。 如果索引鍵不存在於指定的區段中，則會加以建立。 如果這個引數為 Null，則會刪除整個區段，包括區段內的所有專案。  
  
 *lpszString*  
 源指向要寫入檔案的以 null 結束的字串。 如果這個引數為 Null，就會刪除*lpszEntry*引數所指向的索引鍵。  
  
 *lpszFilename*  
 輸出指向以 null 終止的字串，其名稱為初始化檔。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWritePrivateProfileString**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|無法寫入要求的系統資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLWritePrivateProfileString**是用來將驅動程式和驅動程式安裝 Dll 從 Microsoft® Windows®移植到 MICROSOFT windows NT®/Windows 2000 的簡單方式。 將設定檔字串寫入至 Odbc .ini 檔案的**WritePrivateProfileString**呼叫，應取代為**SQLWritePrivateProfileString**的呼叫。 **SQLWritePrivateProfileString**會呼叫 WIN32® API 中的函式，以將指定的值名稱和資料新增至系統資訊的 Odbc 子機碼。  
  
 [設定模式] 會指出在系統資訊中列出 DSN 值的 Odbc 專案在何處。 如果 DSN 是使用者 DSN （狀態變數是 USERDSN_ONLY），則函式會寫入 HKEY_CURRENT_USER 中的 Odbc 專案。 如果 DSN 是系統 DSN （SYSTEMDSN_ONLY），函式會寫入 HKEY_LOCAL_MACHINE 中的 Odbc 專案。 如果狀態變數是 BOTHDSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從系統資訊取得值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
