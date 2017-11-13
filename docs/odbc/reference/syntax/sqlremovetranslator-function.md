---
title: "SQLRemoveTranslator 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c859eba5dc2b064c595ce57dffa2bde6aeda364e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLRemoveTranslator**移除轉譯器的相關資訊 Odbcinst.ini 一節的系統資訊和遞減的轉譯程式元件使用計數 1。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszTranslator*  
 [輸入]轉譯程式的系統資訊 Odbcinst.ini 索引鍵中註冊的名稱。  
  
 *lpdwUsageCount*  
 [輸出]轉譯程式呼叫此函式之後使用狀態計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊的項目不存在，此函式呼叫時，函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveTranslator**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除的轉譯器的資訊，因為它不存在於登錄或登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszTranslator*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式失敗的驅動程式的使用方式計數遞減。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveTranslator**補充[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)元件使用量函式和更新的系統資訊中的計數。 應該只從安裝應用程式呼叫此函式。  
  
 **SQLRemoveTranslator**將元件使用計數減 1。 如果元件使用計數變成 0，將會移除在系統資訊的轉譯程式項目。 轉譯程式項目位於下的轉譯程式的名稱相同的資訊系統中的下列位置：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**實際上不會移除任何檔案。 呼叫端程式負責刪除檔案，並維護的檔案使用計數。 僅元件使用計數和檔案使用計數已達到零就實際刪除的檔案。 可以刪除某些元件中的檔案，以及其他項目不會刪除，根據是否有遞增檔案使用計數其他應用程式所使用的檔案。  
  
 **SQLRemoveTranslator**也稱為升級的程序的一部分。 如果應用程式偵測到它必須執行升級，而且它先前已安裝驅動程式，應該移除，然後重新安裝驅動程式。 **SQLRemoveTranslator**應該先呼叫以遞減的元件使用計數，然後**SQLInstallTranslatorEx**應該呼叫來遞增元件使用計數。 應用程式安裝程式實體必須取代的舊檔案的新檔案。 檔案使用計數將會維持不變，並使用較舊的版本檔案的其他應用程式現在會使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|安裝的轉譯器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|

