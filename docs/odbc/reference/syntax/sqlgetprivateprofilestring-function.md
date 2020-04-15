---
title: SQLGet 私人設定檔字串功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c12fc8d08535960cbb239c14e017b2ad5faa6c0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303290"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLGetPrivateProfileString**獲取與系統資訊值對應的值或數據的名稱清單。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>引數  
 *lpsz節*  
 [輸入]指定包含鍵名稱的節的 null 連接端的字串。 如果此參數為 NULL,則函數將檔中的所有節名稱複製到提供的緩衝區。  
  
 *lpszEntry*  
 [輸入]包含要檢索其關聯字串的鍵名稱的 null 終止字串。 如果此參數為 NULL,*則 lpszSection*參數指定的節中的所有鍵名都將複製到*RetBuffer*參數指定的緩衝區。  
  
 *lpszDefault*  
 [輸入]指向一個 null 連接端字串,該字串指定給定鍵的預設值,如果在初始化檔中找不到該鍵。 此參數不能為 NULL。  
  
 *RetBuffer*  
 【輸出]指向接收檢索的字串的緩衝區。  
  
 *cbRetBuffer*  
 [輸入]指定*RetBuffer*參數指向的緩衝區的大小(以字元表示)。  
  
 *lpszFile 名稱*  
 [輸入]指向命名初始化檔案的 null 終止字串。 如果此參數不包含檔的完整路徑,則搜索預設目錄。  
  
## <a name="returns"></a>傳回值  
 **SQLGetPrivate ProfileString**傳回整數值,指示讀取的字元數。  
  
## <a name="diagnostics"></a>診斷  
 當對**SQLGetPrivateProfileString**的調用失敗時,可以通過調用**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLGetPrivate ProfileString**作為將驅動程式和驅動程式設置 DLL 從 Microsoft ® Windows ® 移植到 Microsoft Windows NT®/Windows 2000 的簡單方法提供。 從 Odbc.ini 檔中檢索配置檔字串的**GetPrivateProfileString**的呼叫應取代為對**SQLGetPrivateProfileString**的呼叫。 **SQLGetPrivate ProfileString**呼叫 Win32® API 中的函數來檢索與系統資訊 Odbc.ini 子鍵的值對應的值或數據的請求名稱。  
  
 配置模式(由**SQLSetConfigMode**設定)指示 Odbc.ini 條目清單 DSN 值在系統資訊中的位置。 如果 DSN 是使用者 DSN(配置模式USERDSN_ONLY),則函數將從 HKEY_CURRENT_USER 中的 Odbc.ini 條目讀取。 如果 DSN 是系統 DSN(SYSTEMDSN_ONLY),則函數將從 HKEY_LOCAL_MACHINE中的 Odbc.ini 條目讀取。 如果配置模式為 BOTHDSN,則嘗試HKEY_CURRENT_USER,如果配置模式失敗,則使用HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|寫入系統資訊寫入值|[SQLWrite 私有設定檔字串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
