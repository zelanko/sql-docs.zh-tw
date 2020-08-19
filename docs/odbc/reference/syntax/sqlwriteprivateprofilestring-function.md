---
description: SQLWritePrivateProfileString 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1110b60d6dc0ba079804ba8a9f21c06f0c1f78d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420952"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函式
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLWritePrivateProfileString** 會將值名稱和資料寫入系統資訊的 Odbc.ini 子機碼。  
  
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
 輸出指向以 null 終止的字串，其中包含將複製字串的區段名稱。 如果區段不存在，則會建立該區段。 區段的名稱與大小寫無關;字串可以是大寫和小寫字母的任何組合。  
  
 *lpszEntry*  
 輸出指向以 null 終止的字串，其中包含要與字串相關聯的索引鍵名稱。 如果索引鍵不存在於指定的區段中，則會加以建立。 如果這個引數是 Null，則會刪除整個區段（包括區段內的所有專案）。  
  
 *lpszString*  
 輸出指向要寫入檔案的以 null 終止的字串。 如果這個引數為 Null，則會刪除 *lpszEntry* 引數所指向的索引鍵。  
  
 *lpszFilename*  
 出指向以 null 終止的字串，該字串會命名初始化檔。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWritePrivateProfileString**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|無法寫入要求的系統資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLWritePrivateProfileString** 是一種簡單的方式，可將來自 Microsoft® Windows®的驅動程式和驅動程式安裝 dll 移植到 microsoft Windows NT®/Windows 2000。 將設定檔字串寫入 Odbc.ini 檔案的 **WritePrivateProfileString** 呼叫，應取代為 **SQLWritePrivateProfileString**的呼叫。 **SQLWritePrivateProfileString** 會呼叫 WIN32® API 中的函式，將指定的值名稱和資料新增至系統資訊的 Odbc.ini 子機碼。  
  
 設定模式會指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。 如果 DSN 是使用者 DSN (狀態變數是 USERDSN_ONLY) ，則函式會寫入 HKEY_CURRENT_USER 中的 Odbc.ini 專案。 如果 DSN 是系統 DSN (SYSTEMDSN_ONLY) ，則函式會寫入 HKEY_LOCAL_MACHINE 中的 Odbc.ini 專案。 如果狀態變數是 BOTHDSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從系統資訊取得值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
