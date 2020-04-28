---
title: SQLRemoveDSNFromIni 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301797"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函式
**標準**  
 引進的版本： ODBC 1。0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**會從系統資訊中移除資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 源要移除之資料來源的名稱。  
  
## <a name="returns"></a>傳回值  
 如果移除資料來源或資料來源不在 Odbc .ini 檔案中，此函數會傳回 TRUE。 如果無法移除資料來源，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDSNFromIni**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_DSN|不正確 DSN|*LpszDSN*引數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法從登錄中移除 DSN 資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>評價  
 **SQLRemoveDSNFromIni**會從系統資訊的 [ODBC 資料來源] 區段中移除資料來源名稱。 它也會移除系統資訊中的 [資料來源規格] 區段。  
  
 此函式只能從驅動程式安裝程式庫呼叫。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|加入、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|移除預設資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|將資料來源名稱新增至系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
