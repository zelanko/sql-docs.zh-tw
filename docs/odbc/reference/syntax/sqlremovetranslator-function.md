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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301785"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLRemoveTranslator**會從系統資訊的 Odbcinst 區段移除翻譯工具的相關資訊，並將翻譯工具的元件使用量計數遞減1。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszTranslator*  
 源在系統資訊的 Odbcinst 機碼中註冊的翻譯工具名稱。  
  
 *lpdwUsageCount*  
 輸出在呼叫此函式之後，翻譯工具的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。 如果在呼叫此函式時，系統資訊中沒有任何專案存在，此函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveTranslator**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除翻譯工具資訊，因為它不存在於登錄中，或在登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszTranslator*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用量計數|安裝程式無法遞減驅動程式的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>評價  
 **SQLRemoveTranslator**會補充[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)函數，並更新系統資訊中的元件使用計數。 此函式只能從安裝應用程式呼叫。  
  
 **SQLRemoveTranslator**會將元件使用計數遞減1。 如果元件使用計數設為0，系統資訊中的 translator 專案就會被移除。 Translator 專案位於系統資訊的下列位置中，位於 translator 名稱底下：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator**實際上不會移除任何檔案。 呼叫程式會負責刪除檔案，並維護檔案使用計數。 只有在元件使用計數和檔案使用量計數都達到零之後，才會實際刪除檔案。 元件中的某些檔案可以刪除，而其他檔案則不會刪除，這取決於是否有其他應用程式使用檔案使用計數而增加。  
  
 **SQLRemoveTranslator**也會在升級過程中呼叫。 如果應用程式偵測到它必須執行升級，而且先前已安裝驅動程式，則應該移除該驅動程式，然後重新安裝。 應該先呼叫**SQLRemoveTranslator**以遞減元件使用計數，然後再呼叫**SQLInstallTranslatorEx**以遞增元件使用計數。 應用程式安裝程式必須實際以新的檔案取代舊的檔案。 檔案使用計數會維持不變，而使用舊版檔案的其他應用程式現在會使用較新的版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝翻譯工具|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
