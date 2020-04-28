---
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
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286968"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函式
**標準**  
 引進的版本： ODBC 2。0  
  
 **摘要**  
 **SQLValidDSN**會先檢查資料來源名稱的長度和有效性，再將名稱新增至系統資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 源要檢查的資料來源名稱。  
  
## <a name="returns"></a>傳回值  
 如果資料來源名稱有效，此函數會傳回 TRUE。 如果資料來源名稱無效或函數呼叫失敗，則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLValidDSN**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 只有在函式呼叫失敗時，才會傳回* \*pfErrorCode* ，如果因為資料來源名稱無效而傳回 FALSE，則不會傳回。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>評價  
 **SQLValidDSN**是由驅動程式的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)呼叫，以檢查資料來源名稱的長度和資料來源名稱中的個別字元有效性。 它會檢查名稱的長度是否大於 SQL_MAX_DSN_LENGTH （如 Sqlext.h 中所定義）。 （ [SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)也會檢查資料來源名稱的長度）。**SQLValidDSN**會檢查資料來源名稱中是否包含下列其中一個不正確字元：  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安裝程式 DLL 中）|  
|加入、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|將資料來源名稱寫入系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
