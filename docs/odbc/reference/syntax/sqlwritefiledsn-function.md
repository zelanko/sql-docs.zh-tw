---
title: SQLWriteFileDSN 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286878"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**將資訊寫入檔 DSN。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>引數  
 *lpszFile 名稱*  
 [輸入]指向檔 DSN 的名稱的指標。 DSN 擴展名將追加到尚未具有 DSN 擴展名的所有檔名中。  
  
 *lpszApp 名稱*  
 [輸入]指向應用程式名稱的指標。 這是 ODBC 部分的「ODBC」。  
  
 *lpszKey名稱*  
 [輸入]指向要讀取的鍵的名稱的指標。 有關保留關鍵字,請參閱"註釋"。  
  
 *lpszString*  
 【輸出]指向與要寫入的鍵關聯的字串。 此參數指向的字串的最大長度為 32,767 位元組。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteFileDSN**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_PATH|不合法安裝路徑|*lpszFileName*參數中指定的檔名的路徑無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*lpszAppName、lpszKeyName*或*lpszString*參數為*lpszKeyName*NULL。|  
  
## <a name="comments"></a>註解  
 ODBC 保留用於儲存連接資訊的節名稱 [ODBC]。 本節的保留關鍵字與**SQLDriverConnect**中為連接字串保留的關鍵字相同。 (有關詳細資訊,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函數說明。  
  
 應用程式可以使用這些保留的關鍵字將資訊直接寫入文件 DSN。 如果應用程式想要建立或修改與檔案 DSN 關聯的 DSN 連接字串,則可以為 [ODBC] 部分中的任何保留連接字串關鍵字調用**SQLWriteFileDSN。**  
  
 如果*lpszString*參數是空指標,則*lpszKeyName*參數指向的關鍵字將從 .dsn 檔中刪除。 如果*lpszString*和*lpszKeyName*參數都是空指標,則*lpszAppName*參數指向的節將從 .dsn 檔中刪除。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|從檔案 DSN 讀取資訊|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
