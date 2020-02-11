---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a86d958114a0755d8aead4470936115902f9c57a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68024548"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函式
**標準**  
 引進的版本： ODBC 3。0  
  
 **摘要**  
 **SQLRemoveDriver**會在系統資訊的 Odbcinst 專案中變更或移除驅動程式的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDriver*  
 源在系統資訊的 Odbcinst 機碼中註冊的驅動程式名稱。  
  
 *fRemoveDSN*  
 源有效的值為：  
  
 TRUE：移除與*lpszDriver*中指定之驅動程式相關聯的 dsn。 FALSE：請勿移除與*lpszDriver*中指定之驅動程式相關聯的 dsn。  
  
 *lpdwUsageCount*  
 輸出在呼叫此函式之後，驅動程式的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。 如果在呼叫此函式時，系統資訊中沒有任何專案存在，此函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriver**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除驅動程式資訊，因為它可能不存在於登錄中，或在登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszDriver*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用量計數|安裝程式無法遞減驅動程式的使用計數。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|*FRemoveDSN*引數為 TRUE;不過，無法移除一或多個 Dsn。 ODBC_REMOVE_DRIVER 要求呼叫**SQLConfigDriver**失敗。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriver**會補充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)函數，並更新系統資訊中的元件使用計數。 此函式只能從安裝應用程式呼叫。  
  
 **SQLRemoveDriver**會將元件使用計數值遞減1。 如果元件使用計數變成0，將會發生下列情況：  
  
1.  將會呼叫具有 ODBC_REMOVE_DRIVER 選項的**SQLConfigDriver**函數。 如果*fRemoveDSN*選項設定為 TRUE， **ConfigDSN**函數會呼叫**SQLRemoveDSNFromIni**來移除與 lpszDriver 中指定之驅動程式相關聯的所有資料來源 *。* 如果*fRemoveDSN*選項設定為 FALSE，則不會刪除資料來源。  
  
2.  系統資訊中的驅動程式專案將會移除。 驅動程式專案位於下列系統資訊位置的驅動程式名稱底下：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**實際上不會移除任何檔案。 呼叫程式會負責刪除檔案及維護檔案使用計數。 只有在元件使用計數和檔案使用量計數都達到零之後，才會實際刪除檔案。 元件中的某些檔案可以刪除，而其他檔案則不會刪除，這取決於是否有其他應用程式使用檔案使用計數而增加。  
  
 **SQLRemoveDriver**也會在升級過程中呼叫。 如果應用程式偵測到它必須執行升級，而且先前已安裝驅動程式，則應該移除該驅動程式，然後重新安裝。 應該先呼叫**SQLRemoveDriver**以遞減元件使用計數，然後再呼叫**SQLInstallDriverEx**以遞增元件使用計數。 應用程式安裝程式必須以新的檔案取代舊的檔案。 檔案使用計數會維持不變，而使用舊版檔案的其他應用程式現在會使用較新的版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) （在安裝程式 DLL 中）|  
|新增、修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
