---
title: SQLGetConfigMode 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54c8dbed5599952778ca7651acbdb55a21b8f876
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206577"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**擷取表示列出資料來源名稱值的 Odbc.ini 項目中的系統資訊的組態模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *pwConfigMode*  
 [輸出]包含組態模式緩衝區的指標。 （請參閱 「 註解。"）中的值 *\*pwConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConfigMode**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 此函式用來判斷列出資料來源名稱值的 Odbc.ini 項目中的系統資訊。 如果 *\*pwConfigMode* ODBC_USER_DSN，資料來源名稱是 「 使用者 DSN，和函式會讀取 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果是 ODBC_SYSTEM_DSN，DSN 為系統 DSN 和函式會讀取在 HKEY_LOCAL_MACHINE 的 Odbc.ini 項目。 如果是 ODBC_BOTH_DSN，HKEY_CURRENT_USER 時嘗試，而且如果失敗，會使用 HKEY_LOCAL_MACHINE。  
  
 根據預設， **SQLGetConfigMode**傳回 ODBC_BOTH_DSN。 「 使用者 DSN 」 或 「 系統 DSN 的呼叫所建立時**SQLConfigDataSource**，函式會將組態模式設為 ODBC_USER_DSN 或 ODBC_SYSTEM_DSN 來區別時修改資料來源名稱的使用者和系統 Dsn。 傳回前, **SQLConfigDataSource**將組態模式重設 ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|設定組態模式|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
