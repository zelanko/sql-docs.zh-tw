---
description: SQLWriteFileDSN 函式
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
ms.openlocfilehash: 4bd63c368f4055821df41faceb7b9c33cf20bde3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421002"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLWriteFileDSN** 會將資訊寫入檔案 DSN。  
  
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
 輸出檔案 DSN 名稱的指標。 DSN 延伸模組會附加至所有尚未具有 DSN 延伸模組的檔案名。  
  
 *lpszAppName*  
 輸出應用程式名稱的指標。 這是 ODBC 區段的 "ODBC"。  
  
 *lpszKeyName*  
 輸出要讀取之索引鍵名稱的指標。 請參閱保留關鍵字的「批註」。  
  
 *lpszString*  
 出指向要寫入的索引鍵相關聯的字串。 此引數所指向之字串的最大長度為32767個位元組。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteFileDSN**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_PATH|不正確安裝路徑|*LpszFileName*引數中指定之檔案名的路徑無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*LpszAppName*、 *lpszKeyName*或*lpszString*引數為 Null。|  
  
## <a name="comments"></a>註解  
 ODBC 會保留區段名稱 [ODBC] 以儲存連接資訊。 此區段的保留關鍵字與針對 **SQLDriverConnect**中的連接字串保留的關鍵字相同。  (需詳細資訊，請參閱 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 函數描述。 )   
  
 應用程式可以使用這些保留的關鍵字，直接將資訊寫入檔案 DSN。 如果應用程式想要建立或修改與 File DSN 相關聯的無 DSN 連接字串，它可以針對 [ODBC] 區段中任何保留的連接字串關鍵字呼叫 **SQLWriteFileDSN** 。  
  
 如果 *lpszString* 引數為 null 指標，則會從 dsn 檔案中刪除 *lpszKeyName* 引數所指向的關鍵字。 如果 *lpszString* 和 *lpszKeyName* 引數都是 null 指標，則會從 Dsn 檔案中刪除 *lpszAppName* 引數所指向的區段。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從 File Dsn 讀取資訊|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
