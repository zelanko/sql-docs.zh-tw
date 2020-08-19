---
description: SQLValidDSN 函式
title: SQLValidDSN 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4919887a6e0bad4526959d0cd31205019a597a0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421022"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函式
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLValidDSN** 會在將名稱加入系統資訊之前，檢查資料來源名稱的長度和有效性。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 輸出要檢查的資料來源名稱。  
  
## <a name="returns"></a>傳回  
 如果資料來源名稱有效，函數會傳回 TRUE。 如果資料來源名稱無效或函式呼叫失敗，則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLValidDSN**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 只有當函式呼叫失敗時，才會傳回* \* pfErrorCode* ，而如果因為資料來源名稱無效而傳回 FALSE，則不會傳回。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 驅動程式的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)會呼叫**SQLValidDSN**來檢查資料來源名稱的長度，以及資料來源名稱中個別字元的有效性。 它會檢查名稱的長度是否大於 SQL_MAX_DSN_LENGTH，如 Sqlext.h 中所定義。  (資料來源名稱的長度也會由 [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)檢查。 ) **SQLValidDSN** 會檢查資料來源名稱中是否包含下列任何不正確字元：  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|安裝 DLL 中的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) () |  
|加入、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|將資料來源名稱寫入系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
