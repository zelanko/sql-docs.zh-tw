---
description: SQLGetPrivateProfileString 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2223d46d507df2a9cf82e7feb800caf5b8f82cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421232"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 函式
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLGetPrivateProfileString** 會取得值的清單，或對應至系統資訊值的資料名稱。  
  
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
 輸出指向以 null 終止的字串，這個字串會指定包含索引鍵名稱的區段。 如果這個引數是 Null，則函式會將檔案中的所有區段名稱複製到提供的緩衝區。  
  
 *lpszEntry*  
 輸出指向以 null 終止的字串，其中包含要抓取其相關聯字串的索引鍵名稱。 如果這個引數是 Null，則 *lpszSection* 引數所指定之區段中的所有索引鍵名稱都會複製到 *RetBuffer* 引數所指定的緩衝區。  
  
 *lpszDefault*  
 輸出指向以 null 終止的字串，這個字串會指定指定之索引鍵的預設值（如果在初始化檔中找不到索引鍵）。 這個引數不可以是 Null。  
  
 *RetBuffer*  
 出指向接收抓取字串的緩衝區。  
  
 *cbRetBuffer*  
 輸出指定 *RetBuffer* 引數所指向之緩衝區的大小（以字元為單位）。  
  
 *lpszFilename*  
 輸出指向以 null 終止的字串，該字串會命名初始化檔。 如果這個引數未包含檔案的完整路徑，則會搜尋預設目錄。  
  
## <a name="returns"></a>傳回  
 **SQLGetPrivateProfileString** 會傳回整數值，指出讀取的字元數。  
  
## <a name="diagnostics"></a>診斷  
 呼叫**SQLGetPrivateProfileString**失敗時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLGetPrivateProfileString** 是一種簡單的方式，可將來自 Microsoft® Windows®的驅動程式和驅動程式安裝 dll 移植到 microsoft Windows NT®/Windows 2000。 從 Odbc.ini 檔案中取出設定檔字串的呼叫 **GetPrivateProfileString** ，應取代為 **SQLGetPrivateProfileString**的呼叫。 **SQLGetPrivateProfileString** 會呼叫 WIN32® API 中的函式，以抓取與系統資訊 Odbc.ini 子機碼值對應的值或資料的要求名稱。  
  
 設定模式 (如 **SQLSetConfigMode** 所設定) 會指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。 如果 DSN 是使用者 DSN (設定模式 USERDSN_ONLY) ，則函式會從 HKEY_CURRENT_USER 的 Odbc.ini 專案中讀取。 如果 DSN 是系統 DSN (SYSTEMDSN_ONLY) ，則函式會從 HKEY_LOCAL_MACHINE 的 Odbc.ini 專案中讀取。 如果設定模式為 BOTHDSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將值寫入系統資訊|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
