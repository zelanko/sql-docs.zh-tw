---
description: SQLGetConfigMode 函式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75093ddb5b33427ac2dc86c3d31fa635a2899118
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491243"
---
# <a name="sqlgetconfigmode-function"></a>SQLGetConfigMode 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLGetConfigMode** 會抓取設定模式，這個模式會指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetConfigMode(  
     UWORD *   pwConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *pwConfigMode*  
 出包含設定模式的緩衝區指標。  (請參閱「批註」。) * \* PwConfigMode*中的值可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetConfigMode**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 此函數是用來判斷在系統資訊中列出 DSN 值的 Odbc.ini 專案。 如果* \* pwConfigMode*為 ODBC_USER_DSN，則 DSN 是使用者 dsn，而函式會從 HKEY_CURRENT_USER 中的 Odbc.ini 專案中讀取。 如果 ODBC_SYSTEM_DSN，則 DSN 是系統 DSN，而函式會從 HKEY_LOCAL_MACHINE 中的 Odbc.ini 專案讀取。 如果 ODBC_BOTH_DSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
 根據預設， **SQLGetConfigMode** 會傳回 ODBC_BOTH_DSN。 當使用者 DSN 或系統 DSN 由呼叫 **SQLConfigDataSource**建立時，此函式會將設定模式設定為 ODBC_USER_DSN 或 ODBC_SYSTEM_DSN，以在修改 DSN 時區分使用者和系統 dsn。 在傳回之前， **SQLConfigDataSource** 會將設定模式重設為 ODBC_BOTH_DSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|設定組態模式|[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|
