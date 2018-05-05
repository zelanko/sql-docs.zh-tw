---
title: SQLWritePrivateProfileString 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd2ef7d8e5fdab610c5bc37f9e58c1dd031b80e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函式
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivateProfileString**寫入系統資訊的 Odbc.ini 子機碼中的值名稱和資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>引數  
 *lpszSection*  
 [輸入]指向以 null 終止的字串，包含要複製字串之區段的名稱。 如果區段不存在，則會建立它。 區段的名稱與大小寫無關;字串可以是任何大寫和小寫字母。  
  
 *lpszEntry*  
 [輸入]指向以 null 終止的字串，包含要與字串相關聯金鑰的名稱。 如果索引鍵不存在指定的區段中，它會建立它。 如果這個引數為 NULL，則會刪除整個區段中，包括區段內的所有項目。  
  
 *lpszString*  
 [輸入]指向以 null 結束的字串寫入檔案。 這個引數為 NULL，如果索引鍵所指向*lpszEntry*引數會被刪除。  
  
 *lpszFilename*  
 [輸出]指向以 null 結束的字串之名稱的初始設定檔案。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWritePrivateProfileString**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|無法寫入要求的系統資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLWritePrivateProfileString**做為 Microsoft Windows/Windows 2000 的連接埠驅動程式和驅動程式安裝 Dll 從 Microsoft® Windows® 簡單的方式。 呼叫**WritePrivateProfileString**寫入 Odbc.ini 檔案的設定檔字串應該取代成呼叫**SQLWritePrivateProfileString**。 **SQLWritePrivateProfileString** Win32® API 加入指定的值名稱和資料的系統資訊的 Odbc.ini 子機碼中呼叫函式。  
  
 組態模式指出列出 DSN 值的 Odbc.ini 項目所在的系統資訊。 如果資料來源名稱 （狀態變數是 USERDSN_ONLY） 為使用者 DSN，函式會寫入在 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果資料來源名稱是系統 DSN (SYSTEMDSN_ONLY)，函式會寫入在 HKEY_LOCAL_MACHINE 的 Odbc.ini 項目。 如果 BOTHDSN 狀態變數，HKEY_CURRENT_USER 時嘗試，而且如果失敗，就會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得系統資訊的值。|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
