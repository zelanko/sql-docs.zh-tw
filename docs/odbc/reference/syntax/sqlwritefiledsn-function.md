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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8b1ce34074a2326d17a199537b308a9a670d8163
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039434"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**將資訊寫入至檔案 DSN。  
  
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
 [輸入]檔案 DSN 名稱的指標。 尚無 DSN 延伸模組的所有檔案名稱會加都上 DSN 延伸模組。  
  
 *lpszAppName*  
 [輸入]應用程式名稱的指標。 這是"ODBC"ODBC 」 一節。  
  
 *lpszKeyName*  
 [輸入]要讀取之索引鍵名稱的指標。 保留關鍵字，請參閱 「 註解 」。  
  
 *lpszString*  
 [輸出]指向要寫入的索引鍵相關聯的字串。 此引數所指向的最大長度是字串的 32,767 個位元組。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteFileDSN**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|中指定的檔案名稱的路徑*lpszFileName*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*LpszAppName*， *lpszKeyName*，或*lpszString*引數為 NULL。|  
  
## <a name="comments"></a>註解  
 ODBC 保留的區段名稱 [ODBC]，用來儲存連接資訊。 本節中的保留的關鍵字和是相同的連接字串中保留**SQLDriverConnect**。 (如需詳細資訊，請參閱 < [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)  
  
 應用程式可以直接將資訊寫入檔案 DSN 中使用這些保留的關鍵字。 如果應用程式想要建立或修改關聯的檔案 DSN 的無 DSN 連接字串，它可以呼叫**SQLWriteFileDSN**任何保留的連接字串關鍵字的 [ODBC] 區段中。  
  
 如果*lpszString*引數是 null 指標，指向關鍵字*lpszKeyName*引數將會刪除從.dsn 檔案。 如果*lpszString*並*lpszKeyName*引數都是 null 指標，指向區段*lpszAppName*引數將會刪除從.dsn 檔案。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|讀取檔案名稱 （dsn） 中的資訊|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
