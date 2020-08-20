---
description: SQLRemoveDriver 函式
title: SQLRemoveDriver 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 503fadfae168a2fc7259cd0507b283563d681bf7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487066"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函式
**一致性**  
 引進的版本： ODBC 3。0  
  
 **總結**  
 **SQLRemoveDriver** 會從系統資訊中的 Odbcinst.ini 專案變更或移除驅動程式的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDriver*  
 輸出在系統資訊的 Odbcinst.ini 金鑰中註冊的驅動程式名稱。  
  
 *fRemoveDSN*  
 輸出有效的值為：  
  
 TRUE：移除與 *lpszDriver*中指定的驅動程式相關聯的 dsn。 FALSE：請勿移除與 *lpszDriver*中指定的驅動程式相關聯的 dsn。  
  
 *lpdwUsageCount*  
 出呼叫此函式之後的驅動程式使用計數。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。 如果在呼叫此函數時，系統資訊中沒有任何專案，則函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriver**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除驅動程式資訊，因為它不存在於登錄中或在登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszDriver*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式無法遞減驅動程式的使用計數。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|*FRemoveDSN*引數為 TRUE;但是，無法移除一或多個 Dsn。 使用 ODBC_REMOVE_DRIVER 要求進行 **SQLConfigDriver** 的呼叫失敗。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriver** 會補充 [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) 函式，並更新系統資訊中的元件使用計數。 您只能從安裝應用程式呼叫此函式。  
  
 **SQLRemoveDriver** 會將元件使用計數值遞減1。 如果元件使用計數變成0，將會發生下列情況：  
  
1.  將會呼叫具有 ODBC_REMOVE_DRIVER 選項的 **SQLConfigDriver** 函數。 如果 *fRemoveDSN* 選項設定為 TRUE，則 **ConfigDSN** 函數會呼叫 **SQLRemoveDSNFromIni** ，以移除與 lpszDriver 中指定之驅動程式相關聯的所有資料來源 *。* 如果 *fRemoveDSN* 選項設定為 FALSE，則不會刪除資料來源。  
  
2.  系統資訊中的驅動程式專案將會移除。 驅動程式專案位於下列系統資訊位置的驅動程式名稱底下：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** 並不會實際移除任何檔案。 呼叫程式會負責刪除檔案和維護檔案使用計數。 只有在元件使用計數和檔案使用次數達到零之後，才會實際刪除檔案。 元件中的某些檔案可以被刪除，而其他檔案則不會被刪除，視檔案使用次數是否已增加的其他應用程式而定。  
  
 **SQLRemoveDriver** 也會在升級過程中被呼叫。 如果應用程式偵測到它必須執行升級，但先前已安裝驅動程式，則應該移除驅動程式，然後再重新安裝。 應先呼叫**SQLRemoveDriver**來遞減元件使用計數，然後再呼叫**SQLInstallDriverEx**來遞增元件的使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數將保持不變，而其他使用舊版檔案的應用程式現在會使用較新的版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|安裝 DLL 中的[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) () |  
|新增、修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
