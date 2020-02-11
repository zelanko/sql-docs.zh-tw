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
ms.openlocfilehash: 6d58fe69e487b4f61384f9bd146b17c6d9ada9ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061467"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函式
**標準**  
 引進的版本： ODBC 2。0  
  
 **摘要**  
 **SQLGetPrivateProfileString**會取得值的名稱清單，或對應到系統資訊值的資料。  
  
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
 *lpszSection*  
 源指向以 null 終止的字串，指定包含索引鍵名稱的區段。 如果這個引數為 Null，函數會將檔案中的所有區段名稱複製到提供的緩衝區。  
  
 *lpszEntry*  
 源指向以 null 終止的字串，其中包含要抓取其相關聯字串的索引鍵名稱。 如果這個引數為 Null，則*lpszSection*引數所指定之區段中的所有索引鍵名稱都會複製到*RetBuffer*引數所指定的緩衝區。  
  
 *lpszDefault*  
 源指向以 null 終止的字串，如果在初始化檔中找不到索引鍵，則會指定給定索引鍵的預設值。 這個引數不可以是 Null。  
  
 *RetBuffer*  
 輸出指向接收已抓取字串的緩衝區。  
  
 *cbRetBuffer*  
 源指定*RetBuffer*引數所指向之緩衝區的大小（以字元為單位）。  
  
 *lpszFilename*  
 源指向以 null 終止的字串，其名稱為初始化檔。 如果這個引數不包含檔案的完整路徑，則會搜尋預設目錄。  
  
## <a name="returns"></a>傳回值  
 **SQLGetPrivateProfileString**會傳回一個整數值，指出讀取的字元數。  
  
## <a name="diagnostics"></a>診斷  
 呼叫**SQLGetPrivateProfileString**失敗時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLGetPrivateProfileString**是用來將驅動程式和驅動程式安裝 Dll 從 Microsoft® Windows®移植到 MICROSOFT windows NT®/Windows 2000 的簡單方式。 從 Odbc .ini 檔案抓取設定檔字串的**GetPrivateProfileString**呼叫，應取代為**SQLGetPrivateProfileString**的呼叫。 **SQLGetPrivateProfileString**會呼叫 WIN32® API 中的函式，以抓取與系統資訊的 Odbc 子機碼值對應的值或資料的要求名稱。  
  
 設定模式（如**SQLSetConfigMode**所設定）表示在系統資訊中列出 DSN 值的 Odbc .ini 專案。 如果 DSN 是使用者 DSN （設定模式是 USERDSN_ONLY），則函式會從 HKEY_CURRENT_USER 中的 Odbc 專案讀取。 如果 DSN 是系統 DSN （SYSTEMDSN_ONLY），函式會從 HKEY_LOCAL_MACHINE 中的 Odbc 專案讀取。 如果設定模式是 BOTHDSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將值寫入系統資訊|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
