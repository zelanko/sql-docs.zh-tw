---
title: SQL移除驅動程式功能 |微軟文件
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
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303929"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 函式
**一致性**  
 版本介紹: ODBC 3.0  
  
 **摘要**  
 **SQLRemoveDriver**更改或刪除系統資訊中的Odbcinst.ini條目中有關驅動程式的資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDriver*  
 [輸入]在系統資訊的 Odbcinst.ini 密鑰中註冊的驅動程式的名稱。  
  
 *f 移除DSN*  
 [輸入]有效值為:  
  
 TRUE:刪除與*lpszDriver*中指定的驅動程式關聯的 DSN。 FALSE:不要刪除與*lpszDriver*中指定的驅動程式關聯的 DSN。  
  
 *lpdwUsage( M) Counts*  
 【輸出]調用此函數後驅動程式的使用計數。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。 如果在調用此函數時系統資訊中不存在條目,則函數將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRemoveDriver**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式*碼值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|註冊表中找不到元件|安裝程式無法刪除驅動程式資訊,因為它要麼不存在在註冊表中,要麼在註冊表中找不到。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|無法增加或遞減元件使用量計數|安裝程式未能減少驅動程式的使用計數。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|*fRemoveDSN*參數為 TRUE;但是,無法刪除一個或多個 DSN。 對**SQLConfigDriver**的呼叫ODBC_REMOVE_DRIVER請求失敗。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLRemoveDriver**補充[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)功能,並更新系統資訊中的元件使用方式計數。 應僅從設置應用程式調用此功能。  
  
 **SQLRemoveDriver**將元件使用計數值減少 1。 如果元件使用計數為 0,則會發生以下情況:  
  
1.  將調用帶有ODBC_REMOVE_DRIVER選項的**SQLConfigDriver**函數。 如果*fRemoveDSN*選項設定為 TRUE,**則 ConfigDSN**函數將呼叫**SQLRemoveDSN FromIni**以刪除與*lpszDriver*中指定的驅動程式關聯的所有資料來源。 如果*fRemoveDSN*選項設定為 FALSE,則不會刪除數據來源。  
  
2.  系統資訊中的驅動程式條目將被刪除。 驅動程式項目位於以下系統資訊位置,在驅動程式名稱下:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver**實際上不會刪除任何檔。 呼叫程式負責刪除檔案和維護檔案使用方式計數。 只有在元件使用計數和檔使用計數都達到零后,才會物理刪除檔。 元件中的某些檔可以刪除,而其他檔不會刪除,具體取決於其他應用程式是否使用檔案,這些應用程式增加了檔使用量計數。  
  
 **SQLRemoveDriver**也稱為升級過程的一部分。 如果應用程式檢測到必須執行升級,並且以前已安裝驅動程式,則應刪除驅動程式,然後重新安裝驅動程式。 應首先調用**SQLRemoveDriver**來遞減元件使用計數,然後調用**SQLInstallDriverEx**以增加元件使用計數。 應用程式安裝程式必須用新檔取代舊檔。 檔使用方式計數將保持不變,使用舊版本檔的其他應用程式現在將使用較新版本。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[設定驅動程式](../../../odbc/reference/syntax/configdriver-function.md)(在設定 DLL 中)|  
|新增、修改或移除驅動程式|[SQL 設定驅動程式](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|安裝驅動程式|[SQL安裝驅動程式Ex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
