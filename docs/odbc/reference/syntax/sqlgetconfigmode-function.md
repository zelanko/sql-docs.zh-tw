---
title: SQLGetConfigMode 函式 |Microsoft 文件
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
- SQLGetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConfigMode
helpviewer_keywords:
- SQLGetConfigMode function [ODBC]
ms.assetid: b96ab3b8-08d5-4fea-9ffe-e03043efbf2d
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 397f4ef5a2efd8e663544f5e21171c2184db1b30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLGetConfigMode**擷取指出列出 DSN 值的 Odbc.ini 項目中的系統資訊的組態模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *pwConfigMode*  
 [輸出]包含組態模式的緩衝區指標。 （請參閱 「 註解。"）中的值 *\*pwConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConfigMode**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 此函式用來判斷列出 DSN 值的 Odbc.ini 項目中的系統資訊。 如果 *\*pwConfigMode* ODBC_USER_DSN，DSN 為使用者 DSN 而且函式會讀取在 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果是 ODBC_SYSTEM_DSN，DSN 為系統 DSN，並從 Odbc.ini 中的項目 HKEY_LOCAL_MACHINE 的函式讀取。 如果是 ODBC_BOTH_DSN，HKEY_CURRENT_USER 時嘗試，而且如果失敗，就會使用 HKEY_LOCAL_MACHINE。  
  
 根據預設， **SQLGetConfigMode**傳回 ODBC_BOTH_DSN。 使用者 DSN] 或 [系統 DSN 的呼叫所建立時**SQLConfigDataSource**，函式會將組態模式 ODBC_USER_DSN 或 ODBC_SYSTEM_DSN 區別時修改資料來源名稱的使用者和系統 Dsn。 在傳回時之前, **SQLConfigDataSource** ODBC_BOTH_DSN 重設為將設定模式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|設定將設定模式|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
