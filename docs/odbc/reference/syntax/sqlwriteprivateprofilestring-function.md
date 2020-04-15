---
title: SQLWrite 私人設定檔字串功能 |微軟文件
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
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286881"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLWritePrivate ProfileString**將值名稱和數據寫入系統資訊的 Odbc.ini 子鍵。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>引數  
 *lpsz節*  
 [輸入]包含要複製此字串的節的名稱的 null 中止字串。 如果節不存在,則創建該節。 該節的名稱與案例無關;字串可以是大寫字母和小寫字母的任意組合。  
  
 *lpszEntry*  
 [輸入]包含要與字串關聯的鍵名稱的 null 連接端接字串。 如果該鍵在指定的節中不存在,則創建該鍵。 如果此參數為 NULL,則刪除整個節,包括節中的所有項目。  
  
 *lpszString*  
 [輸入]指向要寫入檔案的 null 中止字串。 如果此參數為 NULL,則刪除*lpszEntry*參數指向的鍵。  
  
 *lpszFile 名稱*  
 【輸出]指向命名初始化檔案的 null 終止字串。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWritePrivateProfileString**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|無法寫入請求的系統資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLWritePrivate ProfileString**作為將驅動程式和驅動程式設置 DLL 從 Microsoft ® Windows ® 移植到 Microsoft Windows NT®/Windows 2000 的簡單方法提供。 對**寫入私有配置檔String**的呼叫,將設定檔字串寫入Odbc.ini檔應取代為對**SQLWritePrivateProfileString**的呼叫。 **SQLWritePrivate ProfileString**呼叫 Win32® API 中的函數,將指定的值名稱和資料添加到系統資訊的 Odbc.ini 子鍵。  
  
 設定模式指示 Odbc.ini 條目列表 DSN 值在系統資訊中的位置。 如果 DSN 是使用者 DSN(狀態變數為USERDSN_ONLY),則函數將寫入 HKEY_CURRENT_USER 中的 Odbc.ini 條目。 如果 DSN 是系統 DSN (SYSTEMDSN_ONLY),則函數將寫入 HKEY_LOCAL_MACHINE 中的 Odbc.ini 條目。 如果狀態變數為 BOTHDSN,則嘗試HKEY_CURRENT_USER,如果失敗,則使用HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從系統資訊取得值|[SQLGet 私人設定檔字串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
