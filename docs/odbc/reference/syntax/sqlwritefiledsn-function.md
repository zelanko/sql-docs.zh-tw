---
title: SQLWriteFileDSN 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e781f1be79e0079f33b3d0800c665f5f5e9fda4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286878"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLWriteFileDSN**會將資訊寫入檔案 DSN。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>引數  
 *lpszFileName*  
 源檔案 DSN 名稱的指標。 DSN 延伸模組會附加至尚未擁有 DSN 延伸模組的所有檔案名。  
  
 *lpszAppName*  
 源應用程式名稱的指標。 這是 ODBC 區段的 "ODBC"。  
  
 *lpszKeyName*  
 源要讀取的索引鍵名稱的指標。 請參閱保留關鍵字的「批註」。  
  
 *lpszString*  
 輸出指向與要寫入之索引鍵相關聯的字串。 這個引數所指向之字串的最大長度是32767個位元組。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteFileDSN**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_PATH|安裝路徑無效|*LpszFileName*引數中指定的檔案名路徑無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*LpszAppName*、 *lpszKeyName*或*lpszString*引數為 Null。|  
  
## <a name="comments"></a>評價  
 ODBC 會保留用來儲存連接資訊的區段名稱 [ODBC]。 此區段的保留關鍵字與在**SQLDriverConnect**中保留給連接字串的關鍵字相同。 （如需詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述。）  
  
 應用程式可以使用這些保留的關鍵字，直接將資訊寫入檔案 DSN。 如果應用程式想要建立或修改與檔案 DSN 相關聯的無 DSN 連接字串，它可以針對 [ODBC] 區段中的任何保留連接字串關鍵字呼叫**SQLWriteFileDSN** 。  
  
 如果*lpszString*引數為 null 指標，則*lpszKeyName*引數所指向的關鍵字將會從 dsn 檔案中刪除。 如果*lpszString*和*lpszKeyName*引數都是 Null 指標，則*lpszAppName*引數所指向的區段將會從 dsn 檔案中刪除。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從檔案 Dsn 讀取資訊|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
