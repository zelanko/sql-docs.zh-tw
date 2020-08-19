---
description: SQLWriteDSNToIni 函式
title: SQLWriteDSNToIni 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08a1094d29bbba9dc52974bd1cef5cd6645aa5dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421012"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函式
**一致性**  
 引進的版本： ODBC 1。0  
  
 **總結**  
 **SQLWriteDSNToIni** 會將資料來源新增至系統資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 輸出要加入之資料來源的名稱。  
  
 *lpszDriver*  
 輸出驅動程式描述 (通常會將相關聯的 DBMS 名稱) 呈現給使用者，而不是實體驅動程式名稱。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteDSNToIni**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_DSN|不正確 DSN|*LpszDSN*引數包含對 DSN 不正確字串。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszDriver*引數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法在登錄中建立 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLWriteDSNToIni** 會將資料來源加入系統資訊的 [ODBC 資料來源] 區段。 然後，它會建立資料來源的規格區段，並使用驅動程式 DLL 的名稱做為其值，新增單一關鍵字 (**驅動程式**) 。 如果資料來源規格區段已存在， **SQLWriteDSNToIni** 會在建立新區段之前，先將它移除。  
  
 此函式的呼叫者必須將任何驅動程式特定的關鍵字和值加入系統資訊的資料來源規格區段。  
  
 如果資料來源的名稱是預設值， **SQLWriteDSNToIni** 也會在系統資訊中建立預設的驅動程式規格區段。  
  
 這個函式只能從安裝 DLL 呼叫。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|安裝 DLL 中的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) () |  
|加入、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|從系統資訊中移除資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
