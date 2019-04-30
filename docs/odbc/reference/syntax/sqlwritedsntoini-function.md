---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 197c22a160b30fc9c1958e90470c174e3888a053
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233364"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函式
**合規性**  
 導入的版本：ODBC 1.0  
  
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
 [輸入]驅動程式描述 （通常是相關聯的 DBMS 的名稱） 呈現給使用者，而不是實體的驅動程式名稱。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteDSNToIni**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_DSN|無效的資料來源名稱|*LpszDSN*引數包含無效的資料來源名稱的字串。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszDriver*引數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法在登錄中建立的 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLWriteDSNToIni**將系統資訊 [ODBC 資料來源] 區段中的資料來源。 然後會建立資料來源的規格 區段，並將單一關鍵字 (**驅動程式**) 驅動程式 DLL 做為其值的名稱。 如果資料來源規格 > 一節已經存在， **SQLWriteDSNToIni**移除舊的區段之前建立新的帳戶。  
  
 此函式的呼叫端必須將任何驅動程式特有的關鍵字和值加入系統資訊的資料來源規格區段。  
  
 如果資料來源的名稱是預設值， **SQLWriteDSNToIni**也會建立預設驅動程式規格的區段，在系統資訊。  
  
 此函式應該呼叫只會從安裝程式 DLL。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)（在安裝程式 DLL 中）|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|移除系統資訊的資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
