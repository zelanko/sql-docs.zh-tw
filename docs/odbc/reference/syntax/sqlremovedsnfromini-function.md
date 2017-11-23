---
title: "SQLRemoveDSNFromIni 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRemoveDSNFromIni
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDSNFromIni
helpviewer_keywords: SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a665635d371b53fe90bca72393afd986881edad6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函式
**一致性**  
 版本引進了： ODBC 1.0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**移除系統資訊的資料來源。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]若要移除的資料來源的名稱。  
  
## <a name="returns"></a>傳回值  
 如果它會移除資料來源或資料來源中的 Odbc.ini 檔案，則函數會傳回 TRUE。 若要移除資料來源時，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDSNFromIni**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_DSN|無效的資料來源名稱|*LpszDSN*引數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式無法從登錄移除 DSN 資訊。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDSNFromIni**系統資訊 [ODBC 資料來源] 區段中移除資料來源名稱。 它也會移除從系統資訊的資料來源規格 > 一節。  
  
 應該只從驅動程式安裝程式庫呼叫此函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|移除預設的資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|加入系統資訊的資料來源名稱|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
