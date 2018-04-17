---
title: SQLRemoveDriver 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c910c862bd24a29ace17a2ec92352917d41699e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLRemoveDriver**變更或移除 Odbcinst.ini 中的項目系統資訊的驅動程式的相關資訊。  
  
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
  
 TRUE： 移除 Dsn 中指定的驅動程式相關聯*lpszDriver*。 FALSE： 不會移除在指定的驅動程式相關聯的名稱 （dsn） *lpszDriver*。  
  
 *lpdwUsageCount*  
 [輸出]驅動程式呼叫此函式之後使用狀態計數。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊的項目不存在，此函式呼叫時，函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriver**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式無法移除驅動程式的資訊，因為它不存在於登錄或登錄中找不到。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法遞增或遞減元件使用計數|安裝程式失敗的驅動程式的使用方式計數遞減。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|*FRemoveDSN*引數為 TRUE; 不過，無法移除一或多個名稱 （dsn）。 若要呼叫**SQLConfigDriver** ODBC_REMOVE_DRIVER 要求失敗。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriver**補充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)元件使用量函式和更新的系統資訊中的計數。 應該只從安裝應用程式呼叫此函式。  
  
 **SQLRemoveDriver**將元件的使用方式計數值減 1。 如果元件使用計數變成 0，會發生下列狀況：  
  
1.  **SQLConfigDriver** ODBC_REMOVE_DRIVER 選項具有函式會呼叫。 如果*fRemoveDSN*選項設定為 TRUE， **ConfigDSN**函式呼叫**SQLRemoveDSNFromIni**移除在指定的驅動程式相關聯的所有資料來源*lpszDriver。* 如果*fRemoveDSN*選項設為 FALSE，則不會刪除資料來源。  
  
2.  將移除驅動程式中的項目系統資訊。 驅動程式項目是在下列系統資訊底下的位置，驅動程式名稱：  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**實際上不會移除任何檔案。 呼叫端程式負責刪除檔案，並維護的檔案使用計數。 僅元件使用計數和檔案使用計數已達到零就實際刪除的檔案。 可以刪除某些元件中的檔案，以及其他項目不會刪除，根據是否有遞增檔案使用計數其他應用程式所使用的檔案。  
  
 **SQLRemoveDriver**也稱為升級的程序的一部分。 如果應用程式偵測到它必須執行升級，而且它先前已安裝驅動程式，應該移除，然後重新安裝驅動程式。 **SQLRemoveDriver**應該先呼叫以遞減的元件使用計數，然後**SQLInstallDriverEx**應該呼叫來遞增元件使用計數。 應用程式安裝程式必須使用新的檔案取代舊的檔案。 檔案使用計數將會維持不變，並使用較舊的版本檔案的其他應用程式現在會使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) （在安裝程式 DLL 中）|  
|新增、 修改或移除驅動程式|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
