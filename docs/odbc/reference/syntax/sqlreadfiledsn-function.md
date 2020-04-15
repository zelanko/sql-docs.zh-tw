---
title: SQLReadFileDSN 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abda956ee7682c9ac49270e8bf69fb039641790
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303949"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLReadFileDSN**從檔 DSN 讀取資訊。  
  
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
 *lpszFile 名稱*  
 [輸入]指向包含 .dsn 檔名稱的數據緩衝區的指標。 .dsn 擴展名將追加到尚未具有 .dsn 擴展名的所有檔名中。 lpszFileName 中的值必須是 null 終止的字串。 * \**  
  
 *lpszApp 名稱*  
 [輸入]指向包含應用程式名稱的數據緩衝區的指標。 這是 ODBC 部分的「ODBC」。 lpszAppName 中的值必須是 null 終止的字串。 * \**  
  
 *lpszKey名稱*  
 [輸入]指向包含要讀取的鍵名稱的數據緩衝區的指標。 有關保留關鍵字,請參閱"註釋"。 lpszAppName 中的值必須是 null 終止的字串。 * \**  
  
 *lpszString*  
 【輸出]指向包含與要讀取的鍵關聯的字串的數據緩衝區的指標。  
  
 如果*\*lpszFileName*是有效的 .dsn 檔名,但*lpszAppName*參數是空指標 *,lpszKeyName*參數是空指標,則*\*lpszString*包含有效應用程式的清單。 如果*\*lpszFileName*是有效的 .dsn 檔名,*\*並且 lpszAppName*是有效的應用程式名稱,但*lpszKeyName*參數是空指標,則*\*lpszString*在 DSN 檔的相應部分中包含有效保留關鍵字的清單,按分號分隔。 如果*\*lpszFileName*是有效的 .dsn 檔名,但*\*lpszAppName*是空指標 *,lpszKeyName*參數是空指標,則*\*lpszString*包含 DSN 檔中各節的清單,按分號分隔。  
  
 *cbString*  
 [輸入]lpszString 緩衝區的長度*\**。  
  
 *pcbString*  
 【輸出]可在*\*lpszString*中返回的位元組總數。 如果可用於返回的位元組數大於或等於*cbString,* 則*\*lpszString*中的輸出字串將被截斷為*cbString*減去 null 終止字元。 *pcbString*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLReadFileDSN**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszString*參數為 NULL。<br /><br /> *cbString*參數小於或等於 0。|  
|ODBC_ERROR_INVALID_PATH|不合法安裝路徑|*lpszFileName*參數中指定的檔名的路徑無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*lpszAppName*參數為 NULL,而*lpszKeyName*參數有效。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|輸出字串被截斷|在*\*lpszString*中傳回的字串被截斷,因為*cbString*中的值小於或等於*\*在 pcbString*中的值。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|該關鍵字不存在於檔 DSN 中。|  
  
## <a name="comments"></a>註解  
 ODBC 保留用於儲存連接資訊的節名稱 [ODBC]。 本節的保留關鍵字與**SQLDriverConnect**中為連接字串保留的關鍵字相同。 (有關詳細資訊,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數說明。  
  
 應用程式可以使用這些保留的關鍵字讀取檔 DSN 中的資訊。 如果應用程式想要找出與檔案 DSN 關聯的 DSN 連接字串,則可以為 [ODBC] 部分中的任何保留連接字串關鍵字調用**SQLReadFileDSN。** 在無 DSN 連接中傳遞的完整連接字串是 [ODBC] 部分中的所有關鍵字(保留和特定於驅動程式)的組合。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將資訊寫入檔案 DSN|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
