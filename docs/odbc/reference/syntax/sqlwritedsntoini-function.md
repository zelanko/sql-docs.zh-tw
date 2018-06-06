---
title: SQLWriteDSNToIni 函式 |Microsoft 文件
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
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a1ee3bdbdc14c01bf267c9dbb64ef10c93dfe1a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函式
**一致性**  
 版本引進了： ODBC 1.0  
  
 **摘要**  
 **SQLWriteDSNToIni**新增資料來源的系統資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要加入的資料來源的名稱。  
  
 *lpszDriver*  
 [輸入]驅動程式說明 （通常是相關聯的 DBMS 名稱） 呈現給使用者，而不是實體的驅動程式名稱。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteDSNToIni**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_DSN|無效的資料來源名稱|*LpszDSN*引數包含無效的資料來源名稱的字串。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法在登錄中建立 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLWriteDSNToIni**系統資訊 [ODBC 資料來源] 區段中加入的資料來源。 然後建立資料來源規格區段，並將單一關鍵字 (**驅動程式**) 的驅動程式做為其值的 DLL 名稱。 如果資料來源規格區段已經存在， **SQLWriteDSNToIni**之前新增的快取中移除舊區段。  
  
 此函式的呼叫端必須將任何驅動程式特有的關鍵字和值加入資料來源規格區段的系統資訊。  
  
 如果資料來源的名稱是預設值， **SQLWriteDSNToIni**也會建立預設驅動程式規格 > 一節，在 系統資訊。  
  
 只會從安裝 DLL，就應該呼叫此函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)（在安裝程式 DLL 中）|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|移除系統資訊的資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
