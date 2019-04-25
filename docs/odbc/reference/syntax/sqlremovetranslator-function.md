---
title: SQLRemoveTranslator 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf81d013ccf449288791b1875752d5b6067770a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465343"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLRemoveTranslator**移除轉譯器的相關資訊 Odbcinst.ini 這一節的系統資訊和遞減，轉譯器元件使用計數 1。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszTranslator*  
 [輸入]轉譯程式註冊中的系統資訊的 Odbcinst.ini 索引鍵的名稱。  
  
 *lpdwUsageCount*  
 [輸出]轉譯程式呼叫此函式之後的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊 中的項目不存在，此函式呼叫時，此函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveTranslator**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到的元件|安裝程式無法移除 translator 資訊，因為在登錄中不存在或找不到登錄中。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszTranslator*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減的元件使用計數|安裝程式無法以遞減的驅動程式的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveTranslator**補充[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)元件使用函式和更新的系統資訊中的計數。 只能從安裝應用程式，就應該呼叫此函式。  
  
 **SQLRemoveTranslator**會減 1 的元件使用計數。 如果元件使用計數變成 0，將會移除在系統資訊中的轉譯程式項目。 轉譯程式項目是在 [系統資訊] 下的 translator 名稱中的下列位置：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**實際上不會移除任何檔案。 呼叫端程式負責刪除檔案，和維護的檔案使用計數。 僅元件使用計數和檔案使用計數已達到零之後實際刪除的檔案。 可以刪除某些元件中的檔案，與其他人不會刪除，取決於是否有遞增檔案使用計數的其他應用程式所使用的檔案。  
  
 **SQLRemoveTranslator**也稱為升級的程序的一部分。 如果應用程式偵測到它必須執行升級，而且它先前已安裝驅動程式，應該移除，然後重新安裝驅動程式。 **SQLRemoveTranslator**第一次應該呼叫以遞減的元件使用計數，然後**SQLInstallTranslatorEx**應該呼叫要遞增的元件使用計數。 應用程式安裝程式必須實際的舊檔案的新檔案取代。 檔案使用計數會維持不變，並使用較舊的版本檔案的其他應用程式現在會使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|安裝的轉譯器|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
