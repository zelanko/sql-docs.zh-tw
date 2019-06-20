---
title: SQLReadFileDSN 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f32e23be700f17fee88cc6354f8652bb1333a12c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537344"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLReadFileDSN**讀取檔案 DSN 中的資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 [輸入]包含.dsn 檔案名稱的資料緩衝區的指標。 還沒有.dsn 延伸模組的所有檔案名稱會加都上副檔名為.dsn。 中的值 *\*lpszFileName*必須是以 null 結束的字串。  
  
 *lpszAppName*  
 [輸入]包含名稱的應用程式的資料緩衝區的指標。 這是"ODBC"ODBC 」 一節。 中的值 *\*lpszAppName*必須是以 null 結束的字串。  
  
 *lpszKeyName*  
 [輸入]包含要讀取之索引鍵名稱的資料緩衝區的指標。 保留關鍵字，請參閱 「 註解 」。 中的值 *\*lpszAppName*必須是以 null 結束的字串。  
  
 *lpszString*  
 [輸出]包含要讀取索引鍵相關聯的字串資料緩衝區的指標。  
  
 如果 *\*lpszFileName*是有效的.dsn 檔案名稱，但*lpszAppName*引數是 null 指標，而*lpszKeyName*引數是 null 指標，則 *\*lpszString*包含有效的應用程式的清單。 如果 *\*lpszFileName*是有效的.dsn 檔案名稱並 *\*lpszAppName*是有效的應用程式的名稱，但*lpszKeyName*引數是 null指標，然後 *\*lpszString*包含有效的 DSN 檔案，請以分號分隔的適當小節中的保留關鍵字的清單。 如果 *\*lpszFileName*是有效的.dsn 檔案名稱，但 *\*lpszAppName*是 null 指標，而*lpszKeyName*引數是 null 指標，然後 *\*lpszString*包含一份在 DSN 檔案中，以分號分隔的區段。  
  
 *cbString*  
 [輸入]長度 *\*lpszString*緩衝區。  
  
 *pcbString*  
 [輸出]傳回在可用的位元組總數 *\*lpszString*。 傳回可用的位元組數目是否大於或等於*cbString*，在輸出字串 *\*lpszString*會被截斷成*cbString*減去null 終止的字元。 *PcbString*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLReadFileDSN**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszString*引數為 NULL。<br /><br /> *CbString*引數小於或等於 0。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|中指定的檔案名稱的路徑*lpszFileName*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*LpszAppName*引數為 NULL，而*lpszKeyName*引數無效。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|截斷的輸出字串|在傳回的字串 *\*lpszString*被截斷，因為中的值*cbString*小於或等於中的值 *\*pcbString*.|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|在 檔案 DSN 中不存在的關鍵字。|  
  
## <a name="comments"></a>註解  
 ODBC 保留的區段名稱 [ODBC]，用來儲存連接資訊。 本節中的保留的關鍵字和是相同的連接字串中保留**SQLDriverConnect**。 (如需詳細資訊，請參閱 < [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)  
  
 應用程式可以使用這些保留的關鍵字來讀取檔案 DSN 中的資訊。 如果應用程式想要找出檔案 DSN 中相關聯的無 DSN 連接字串也可以呼叫**SQLReadFileDSN**任何保留的連接字串關鍵字的 [ODBC] 區段中。 傳入無 DSN 連接的完整連接字串是所有 [ODBC] 區段中的關鍵字 （保留和驅動程式特有） 的組合。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將資訊寫入至檔案 DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
