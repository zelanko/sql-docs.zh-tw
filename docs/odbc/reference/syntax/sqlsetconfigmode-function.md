---
title: SQLSetConfigMode 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c36da48fa1493f61131d23a07f7a820b67ebac82
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293278"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLSetConfigMode**會設定模式，以指出在系統資訊中列出 DSN 值的 Odbc 專案所在的位置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *wConfigMode*  
 源安裝程式設定模式（請參閱「批註」）。 *WConfigMode*中的值可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConfigMode**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*WConfigMode*引數不包含 ODBC_USER_DSN、ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN。|  
  
## <a name="comments"></a>評價  
 此函式是用來設定在系統資訊中列出 DSN 值的 Odbc 專案所在的位置。 如果 ODBC_USER_DSN *wConfigMode* ，dsn 就是使用者 dsn，而函式會從 HKEY_CURRENT_USER 中的 ODBC 專案讀取。 如果 ODBC_SYSTEM_DSN，DSN 就是系統 DSN，而函式會從 HKEY_LOCAL_MACHINE 中的 Odbc 專案讀取。 如果 ODBC_BOTH_DSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
 此函式不會影響**SQLCreateDataSource**和**SQLDriverConnect**。 當驅動程式從登錄讀取時，您必須呼叫**SQLGetPrivateProfileString**或藉由呼叫**SQLWritePrivateProfileString**來寫入登錄，設定模式。 呼叫**SQLGetPrivateProfileString**和**SQLWritePrivateProfileString**時，會使用設定模式來知道要操作的登錄部分。  
  
> [!CAUTION]  
>  只有在必要時才應呼叫**SQLSetConfigMode** ;如果模式設定不正確，ODBC 安裝程式可能無法正常運作。  
  
 **SQLSetConfigMode**會直接修改設定模式。 這與透過呼叫**SQLConfigDataSource**來修改設定模式的程式並不相同。 呼叫**SQLConfigDataSource**時，會設定在修改 DSN 時用來區分使用者和系統 dsn 的配置模式。 在傳回之前， **SQLConfigDataSource**會將設定模式重設為 BOTHDSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|正在抓取設定模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
