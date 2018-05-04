---
title: SQLGetPrivateProfileString 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b25bd5b5c7df80c426542ccd5ca2fe2eab2988a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函式
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLGetPrivateProfileString**取得一份值或資料的系統資訊的值對應的名稱。  
  
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
 [輸入]指向以 null 終止的字串，指定包含索引鍵名稱的區段。 如果這個引數為 NULL，函式會將所有的區段名稱在檔案複製到提供的緩衝區中。  
  
 *lpszEntry*  
 [輸入]指向以 null 結尾字串，包含其相關聯的字串時要擷取的索引鍵名稱。 如果這個引數為 NULL，所有索引鍵中指定之區段的名稱*lpszSection*引數會複製到所指定的緩衝區*RetBuffer*引數。  
  
 *lpszDefault*  
 [輸入]指向以 null 結束的字串，指定預設值，指定索引鍵，如果初始設定檔案中找不到索引鍵。 這個引數不能是 NULL。  
  
 *RetBuffer*  
 [輸出]指向接收擷取的字串的緩衝區。  
  
 *cbRetBuffer*  
 [輸入]指定以字元為單位，所指向之緩衝區的大小， *RetBuffer*引數。  
  
 *lpszFilename*  
 [輸入]指向以 null 結束的字串之名稱的初始設定檔案。 如果這個引數不包含檔案的完整路徑，預設會搜尋的目錄。  
  
## <a name="returns"></a>傳回值  
 **SQLGetPrivateProfileString**傳回整數值，指出讀取的字元數。  
  
## <a name="diagnostics"></a>診斷  
 當呼叫**SQLGetPrivateProfileString**失敗時，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLGetPrivateProfileString**做為 Microsoft Windows/Windows 2000 的連接埠驅動程式和驅動程式安裝 Dll 從 Microsoft® Windows® 簡單的方式。 呼叫**GetPrivateProfileString** Odbc.ini 檔案的設定檔字串應取代該擷取呼叫**SQLGetPrivateProfileString**。 **SQLGetPrivateProfileString** Win32® API 來擷取要求的值或系統資訊的 Odbc.ini 子機碼值對應的資料名稱中呼叫函式。  
  
 將設定模式 (為設定由**SQLSetConfigMode**) 表示列出 DSN 值的 Odbc.ini 項目中的系統資訊。 如果資料來源名稱 （將設定模式是 USERDSN_ONLY） 為使用者 DSN，函式會讀取在 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果資料來源名稱是系統 DSN (SYSTEMDSN_ONLY)，函式會讀取在 HKEY_LOCAL_MACHINE 的 Odbc.ini 項目。 如果 BOTHDSN 組態模式下，HKEY_CURRENT_USER 時嘗試，而且如果失敗，就會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將值寫入系統資訊|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
