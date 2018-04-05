---
title: SQLReadFileDSN 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a21a11c4b7b0ba3991df73e5e3e0860e5d4042b8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLReadFileDSN**檔案 DSN 會讀取資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>引數  
 *lpszFileName*  
 [輸入]包含.dsn 檔案名稱的資料緩衝區的指標。 .Dsn 擴充功能被附加到還沒有.dsn 延伸模組的所有檔案名稱。 中的值 *\*lpszFileName*必須是以 null 結束的字串。  
  
 *lpszAppName*  
 [輸入]包含的應用程式名稱的資料緩衝區的指標。 這是 ODBC 區段是"ODBC"。 中的值 *\*lpszAppName*必須是以 null 結束的字串。  
  
 *lpszKeyName*  
 [輸入]包含要讀取之索引鍵名稱的資料緩衝區的指標。 保留關鍵字，請參閱 「 註解 」。 中的值 *\*lpszAppName*必須是以 null 結束的字串。  
  
 *lpszString*  
 [輸出]資料緩衝區，其中包含要讀取的索引鍵相關聯的字串指標。  
  
 如果 *\*lpszFileName*是有效的.dsn 檔案名稱但*lpszAppName*引數為 null 指標和*lpszKeyName*引數是 null 指標，則 *\*lpszString*包含有效的應用程式的清單。 如果 *\*lpszFileName*是有效的.dsn 檔案名稱和 *\*lpszAppName*是有效的應用程式的名稱，但*lpszKeyName*引數是 null指標，然後 *\*lpszString*包含有效的 DSN 檔案，請以分號分隔的適當章節中的保留關鍵字的清單。 如果 *\*lpszFileName*是有效的.dsn 檔案名稱，但 *\*lpszAppName*為 null 指標和*lpszKeyName*引數是 null 指標，然後 *\*lpszString*包含一份在 DSN 檔案中，以分號分隔的區段。  
  
 *cbString*  
 [輸入]長度 *\*lpszString*緩衝區。  
  
 *pcbString*  
 [輸出]可用來傳回中的位元組總數 *\*lpszString*。 如果傳回可用的位元組數目大於或等於*cbString*，輸出字串中的 *\*lpszString*會被截斷成*cbString*減號null 結束的字元。 *PcbString*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLReadFileDSN**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszString*引數為 NULL。<br /><br /> *CbString*引數以前是小於或等於 0。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|檔案名稱中指定的路徑*lpszFileName*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*LpszAppName*引數為 NULL，而*lpszKeyName*是有效的引數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|輸出字串截斷|在傳回的字串 *\*lpszString*被截斷，因為中的值*cbString*小於或等於中的值 *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|關鍵字不存在於檔案 DSN。|  
  
## <a name="comments"></a>註解  
 ODBC 保留的區段名稱 [ODBC]，用來儲存連接資訊。 本章節的保留的關鍵字和是相同的連接字串中保留**SQLDriverConnect**。 (如需詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)  
  
 應用程式可以使用這些保留的關鍵字來讀取檔案 DSN 中的資訊。 如果應用程式想要找出無 dsn 連接字串相關聯檔案 DSN，它可以呼叫**SQLReadFileDSN**任何 [ODBC] 區段中保留的連接字串關鍵字。 無 dsn 連接傳入的完整連接字串是所有 [ODBC] 區段中的關鍵字 （保留和驅動程式特有） 的組合。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將資訊寫入至檔案 DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
