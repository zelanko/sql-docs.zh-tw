---
title: SQLGetPrivateProfileString 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77d1f433732cf710e715418df94eba5184e9a907
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132673"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函式
**合規性**  
 導入的版本：ODBC 2.0  
  
 **摘要**  
 **SQLGetPrivateProfileString**取得一份名稱的值或系統資訊的值相對應的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>引數  
 *lpszSection*  
 [輸入]指向以 null 終止的字串，指定包含索引鍵名稱的區段。 如果這個引數為 NULL，函式會將所有的區段名稱中的檔案複製到提供的緩衝區中。  
  
 *lpszEntry*  
 [輸入]指向以 null 結尾字串，包含其相關聯的字串是要擷取的索引鍵名稱。 如果這個引數為 NULL，所有索引鍵名稱在指定之區段*lpszSection*引數會複製到所指定的緩衝區*RetBuffer*引數。  
  
 *lpszDefault*  
 [輸入]指向以 null 結束的字串，指定預設值，指定索引鍵，如果在初始設定檔案中找不到索引鍵。 這個引數不能是 NULL。  
  
 *RetBuffer*  
 [輸出]指向接收擷取的字串的緩衝區。  
  
 *cbRetBuffer*  
 [輸入]指定的大小，以字元為單位所指向的緩衝區*RetBuffer*引數。  
  
 *lpszFilename*  
 [輸入]指向以 null 結束的字串之名稱的初始設定檔案。 如果這個引數不包含檔案的完整路徑，預設會搜尋目錄。  
  
## <a name="returns"></a>傳回值  
 **SQLGetPrivateProfileString**傳回整數值，指出讀取的字元數。  
  
## <a name="diagnostics"></a>診斷  
 當呼叫**SQLGetPrivateProfileString**失敗，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLGetPrivateProfileString**做為 Microsoft Windows/Windows 2000 的連接埠驅動程式和驅動程式安裝程式 Dll 從 Microsoft® Windows® 簡單的方式。 若要呼叫**GetPrivateProfileString** Odbc.ini 檔案的設定檔字串應取代該擷取呼叫**SQLGetPrivateProfileString**。 **SQLGetPrivateProfileString** Win32® API 來擷取要求之的名稱的值或系統資訊中的 Odbc.ini 子機碼值相對應的資料中呼叫函式。  
  
 設定模式 (所設定的**SQLSetConfigMode**) 表示列出資料來源名稱值的 Odbc.ini 項目中的系統資訊。 如果資料來源名稱 （組態模式是 USERDSN_ONLY） 「 使用者 DSN，函式會讀取 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果 DSN 是系統 DSN (SYSTEMDSN_ONLY)，函式會讀取在 HKEY_LOCAL_MACHINE 的 Odbc.ini 項目。 如果 BOTHDSN 組態模式，HKEY_CURRENT_USER 時嘗試，而且如果失敗，會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將值寫入系統資訊|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
