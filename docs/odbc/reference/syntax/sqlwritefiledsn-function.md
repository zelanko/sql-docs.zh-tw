---
title: SQLWriteFileDSN 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36af0a5a3098dd4afc334de6bd808c0c690a601c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918273"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLWriteFileDSN**將資訊寫入至檔案 DSN。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>引數  
 *lpszFileName*  
 [輸入]檔案 DSN 名稱的指標。 DSN 擴充功能被附加至所有尚無 DSN 副檔名的檔案名稱。  
  
 *lpszAppName*  
 [輸入]應用程式名稱的指標。 這是 ODBC 區段是"ODBC"。  
  
 *lpszKeyName*  
 [輸入]要讀取之索引鍵名稱的指標。 保留關鍵字，請參閱 「 註解 」。  
  
 *lpszString*  
 [輸出]指向要寫入索引鍵相關聯的字串。 這個引數指向的字串的最大長度為 32,767 個位元組。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteFileDSN**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_PATH|無效的安裝路徑|檔案名稱中指定的路徑*lpszFileName*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*LpszAppName*， *lpszKeyName*，或*lpszString*引數為 NULL。|  
  
## <a name="comments"></a>註解  
 ODBC 保留的區段名稱 [ODBC]，用來儲存連接資訊。 本章節的保留的關鍵字和是相同的連接字串中保留**SQLDriverConnect**。 (如需詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。)  
  
 應用程式可以直接將資訊寫入檔案 DSN 中使用這些保留的關鍵字。 如果應用程式想要建立或修改檔案 DSN 與關聯的 dsn 連接字串，它可以呼叫**SQLWriteFileDSN**任何 [ODBC] 區段中保留的連接字串關鍵字。  
  
 如果*lpszString*引數為 null 指標，指向關鍵字*lpszKeyName*引數將會刪除從.dsn 檔案。 如果*lpszString*和*lpszKeyName*引數都是 null 指標，一節所指*lpszAppName*引數將會刪除從.dsn 檔案。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|讀取檔案 Dsn 資訊|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
