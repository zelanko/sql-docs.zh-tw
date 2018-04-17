---
title: SQLValidDSN 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71a4eb5f9c41da08631d38e0a282e349e53bdb2a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函式
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLValidDSN**名稱加入至 系統資訊之前，檢查長度和有效的資料來源名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要檢查名稱的資料來源。  
  
## <a name="returns"></a>傳回值  
 如果資料來源名稱無效，函式會傳回 TRUE。 如果資料來源名稱無效，或函式呼叫失敗，則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLValidDSN**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 A  *\*pfErrorCode*會傳回只函式呼叫失敗時，不傳回 FALSE，因為資料來源名稱無效。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLValidDSN**驅動程式會呼叫[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)檢查資料來源名稱的長度，以及資料來源名稱中的個別字元的有效性。 它會檢查是否名稱的長度大於 SQL_MAX_DSN_LENGTH，Sqlext.h 中所定義。 (也會檢查資料來源名稱的長度所[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)。)**SQLValidDSN**檢查任何下列無效的字元是否包含在資料來源名稱：  
  
 [ ] { } ( ) , ; ? * = ! @ \  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安裝程式 DLL 中）|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|系統資訊寫入資料來源名稱|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
