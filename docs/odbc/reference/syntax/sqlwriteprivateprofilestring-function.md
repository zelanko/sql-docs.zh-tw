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
manager: craigg
ms.openlocfilehash: ff853976cf0d900cb24391ff6bf13838782ea876
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536763"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函式
**合規性**  
 導入的版本：ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivateProfileString**寫入 Odbc.ini 子機碼的系統資訊的值名稱和資料。  
  
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
 [輸入]指向以 null 終止的字串，包含要複製的字串區段的名稱。 如果區段不存在，它會建立它。 區段的名稱與大小寫無關;字串可以是任何大寫和小寫字母。  
  
 *lpszEntry*  
 [輸入]指向以 null 終止的字串，包含要與字串相關聯的索引鍵的名稱。 如果索引鍵不存在於指定的區段中，它會建立它。 如果這個引數為 NULL，則會刪除整個區段，包括的區段內的所有項目。  
  
 *lpszString*  
 [輸入]指向以 null 終止的字串寫入至檔案。 如果這個引數為 NULL，索引鍵所指向*lpszEntry*引數會被刪除。  
  
 *lpszFilename*  
 [輸出]指向以 null 結束的字串之名稱的初始設定檔案。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWritePrivateProfileString**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|無法寫入要求的系統資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLWritePrivateProfileString**做為 Microsoft Windows/Windows 2000 的連接埠驅動程式和驅動程式安裝程式 Dll 從 Microsoft® Windows® 簡單的方式。 若要呼叫**WritePrivateProfileString**寫入 Odbc.ini 檔案的設定檔字串應該取代成呼叫**SQLWritePrivateProfileString**。 **SQLWritePrivateProfileString** Win32® API，將指定的值名稱和資料新增至系統資訊中的 Odbc.ini 子機碼中呼叫函式。  
  
 設定模式表示列出資料來源名稱值的 Odbc.ini 項目所在的系統資訊。 如果資料來源名稱 （狀態變數是 USERDSN_ONLY） 「 使用者 DSN，則此函式會寫入 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果 DSN 是系統 DSN (SYSTEMDSN_ONLY)，則此函式會寫入 Odbc.ini 中的項目 HKEY_LOCAL_MACHINE。 如果 BOTHDSN 狀態變數，HKEY_CURRENT_USER 時嘗試，而且如果失敗，會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得系統資訊的值。|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
