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
manager: craigg
ms.openlocfilehash: 3ef98000391ec6c39012603795b7f11a34c68183
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208137"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLRemoveDriver**變更或移除 Odbcinst.ini 中的項目系統資訊中的驅動程式的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDriver*  
 [輸入]在 系統資訊的 Odbcinst.ini 索引鍵中註冊的驅動程式名稱。  
  
 *fRemoveDSN*  
 [輸入]有效值為：  
  
 TRUE:移除在指定的驅動程式相關聯的 Dsn *lpszDriver*。 FALSE:請勿移除在指定的驅動程式相關聯的 Dsn *lpszDriver*。  
  
 *lpdwUsageCount*  
 [輸出]驅動程式在呼叫此函式之後的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊 中的項目不存在，此函式呼叫時，此函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriver**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到的元件|安裝程式無法移除驅動程式的資訊，因為它不存在登錄中，或找不到登錄中。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszDriver*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減的元件使用計數|安裝程式無法以遞減的驅動程式的使用計數。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|*FRemoveDSN*引數為 TRUE; 不過，無法移除一個或多個名稱 （dsn）。 若要在呼叫**SQLConfigDriver** ODBC_REMOVE_DRIVER 要求失敗。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriver**補充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)元件使用函式和更新的系統資訊中的計數。 只能從安裝應用程式，就應該呼叫此函式。  
  
 **SQLRemoveDriver**會減 1 的元件使用方式計數值。 如果元件使用計數變成 0，會發生下列情況：  
  
1.  **SQLConfigDriver** ODBC_REMOVE_DRIVER 選項的函式會呼叫。 如果*fRemoveDSN*選項設定為 TRUE， **ConfigDSN**函式呼叫**SQLRemoveDSNFromIni**移除在指定的驅動程式相關聯的所有資料來源*lpszDriver。* 如果*fRemoveDSN*選項設定為 FALSE，則不會刪除資料來源。  
  
2.  系統資訊 中的驅動程式項目將會移除。 驅動程式項目是在下列系統資訊底下的位置，驅動程式名稱：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**實際上不會移除任何檔案。 呼叫端程式負責刪除檔案和維護的檔案使用計數。 僅元件使用計數和檔案使用計數已達到零之後實際刪除的檔案。 可以刪除某些元件中的檔案，與其他人不會刪除，取決於是否有遞增檔案使用計數的其他應用程式所使用的檔案。  
  
 **SQLRemoveDriver**也稱為升級的程序的一部分。 如果應用程式偵測到它必須執行升級，而且它先前已安裝驅動程式，應該移除，然後重新安裝驅動程式。 **SQLRemoveDriver**第一次應該呼叫以遞減的元件使用計數，然後**SQLInstallDriverEx**應該呼叫要遞增的元件使用計數。 應用程式安裝程式必須以新檔案取代舊的檔案。 檔案使用計數會維持不變，並使用較舊的版本檔案的其他應用程式現在會使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) （在安裝程式 DLL 中）|  
|新增、 修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
