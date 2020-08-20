---
description: SQLRemoveTranslator 函式
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
ms.openlocfilehash: 92042d1a29720d8fcca32d3fb7127f24a0566b7e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499601"
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLRemoveTranslator** 會從系統資訊的 Odbcinst.ini 區段中移除翻譯工具的相關資訊，並將翻譯工具的元件使用量計數遞減1。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszTranslator*  
 輸出以系統資訊的 Odbcinst.ini 金鑰註冊的翻譯工具名稱。  
  
 *lpdwUsageCount*  
 出在呼叫此函式之後，翻譯工具的使用計數。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。 如果在呼叫此函數時，系統資訊中沒有任何專案，則函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveTranslator**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除轉譯程式資訊，因為它不存在於登錄中或在登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszTranslator*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞減驅動程式的使用計數。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveTranslator** 會補充 [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) 函式，並更新系統資訊中的元件使用計數。 您只能從安裝應用程式呼叫此函式。  
  
 **SQLRemoveTranslator** 會將元件使用計數遞減1。 如果元件使用計數變成0，系統資訊中的翻譯工具專案將會被移除。 Translator 專案位於系統資訊中的下列位置，在翻譯工具名稱底下：  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** 並不會實際移除任何檔案。 呼叫程式負責刪除檔案，以及維護檔案使用計數。 只有在元件使用計數和檔案使用次數達到零之後，才會實際刪除檔案。 元件中的某些檔案可以被刪除，而其他檔案則不會被刪除，視檔案使用次數是否已增加的其他應用程式而定。  
  
 **SQLRemoveTranslator** 也會在升級過程中被呼叫。 如果應用程式偵測到它必須執行升級，但先前已安裝驅動程式，則應該移除驅動程式，然後再重新安裝。 應先呼叫**SQLRemoveTranslator**來遞減元件使用計數，然後再呼叫**SQLInstallTranslatorEx**來遞增元件的使用計數。 應用程式安裝程式必須實際以新的檔案取代舊的檔案。 檔案使用計數將保持不變，而其他使用舊版檔案的應用程式現在會使用較新的版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|安裝 translator|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
