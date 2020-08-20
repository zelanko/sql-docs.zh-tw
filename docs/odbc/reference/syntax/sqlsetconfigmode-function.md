---
description: SQLSetConfigMode 函式
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
ms.openlocfilehash: 5aab5274403a654362c5732d8ec3f6eccae3be96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499581"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLSetConfigMode** 會設定設定模式，指出列出 DSN 值的 Odbc.ini 專案在系統資訊中的位置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *wConfigMode*  
 輸出安裝程式設定模式 (查看「批註」 ) 。 *WConfigMode*中的值可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConfigMode**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|不正確參數順序|*WConfigMode*引數未包含 ODBC_USER_DSN、ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN。|  
  
## <a name="comments"></a>註解  
 此函數是用來設定在系統資訊中列出 DSN 值的 Odbc.ini 專案。 如果 *wConfigMode* 為 ODBC_USER_DSN，則 Dsn 是使用者 dsn，而函式會從 HKEY_CURRENT_USER 中的 Odbc.ini 專案中讀取。 如果 ODBC_SYSTEM_DSN，則 DSN 是系統 DSN，而函式會從 HKEY_LOCAL_MACHINE 中的 Odbc.ini 專案讀取。 如果 ODBC_BOTH_DSN，則會嘗試 HKEY_CURRENT_USER，如果失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
 此函數不會影響 **SQLCreateDataSource** 和 **SQLDriverConnect**。 當驅動程式從登錄讀取時，必須藉由呼叫 **SQLGetPrivateProfileString** 或藉由呼叫 **SQLWritePrivateProfileString**寫入登錄，來設定設定模式。 對 **SQLGetPrivateProfileString** 和 **SQLWritePrivateProfileString** 的呼叫會使用設定模式來知道要操作的登錄部分。  
  
> [!CAUTION]  
>  **SQLSetConfigMode** 只能在必要時呼叫;如果模式設定不正確，ODBC 安裝程式可能會無法正常運作。  
  
 **SQLSetConfigMode** 會直接修改設定模式。 這與透過呼叫 **SQLConfigDataSource**來修改設定模式的程式分開。 對 **SQLConfigDataSource** 的呼叫會設定設定模式，以在修改 DSN 時區分使用者和系統 dsn。 在傳回之前， **SQLConfigDataSource** 會將設定模式重設為 BOTHDSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|正在抓取設定模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
