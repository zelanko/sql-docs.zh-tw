---
description: SQLConfigDataSource 函數 (英文)
title: SQLConfigDataSource 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8849ce5528380e4164a420227395bce5aa436eaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448741"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 函數 (英文)
**一致性**  
 引進的版本： ODBC 1。0  
  
 **總結**  
 **SQLConfigDataSource** 會新增、修改或刪除資料來源。  
  
 您也可以使用[ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)來存取**SQLConfigDataSource**的功能。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 輸出父視窗控制碼。 如果控制碼為 null，函數將不會顯示任何對話方塊。  
  
 *fRequest*  
 輸出要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_ADD_DSN：加入新的使用者資料來源。  
  
 ODBC_CONFIG_DSN：設定 (修改現有的使用者資料來源) 。  
  
 ODBC_REMOVE_DSN：移除現有的使用者資料來源。  
  
 ODBC_ADD_SYS_DSN：新增系統資料來源。  
  
 ODBC_CONFIG_SYS_DSN：修改現有的系統資料來源。  
  
 ODBC_REMOVE_SYS_DSN：移除現有的系統資料來源。  
  
 ODBC_REMOVE_DEFAULT_DSN：從系統資訊中移除預設的資料來源規格區段。  (也會從系統資訊中的 Odbcinst.ini 專案移除預設的驅動程式規格區段。 此 *fRequest* 會執行與已被取代的 **SQLRemoveDefaultDataSource** 函式相同的函式。 ) 指定此選項時，呼叫 **SQLConfigDataSource** 的所有其他參數都應該是 null;如果不是 Null，則會忽略它們。  
  
 *lpszDriver*  
 輸出驅動程式描述 (通常會將相關聯的 DBMS 名稱) 呈現給使用者，而不是實體驅動程式名稱。  
  
 *lpszAttributes*  
 輸出雙向以 null 終止的屬性清單（以關鍵字-值配對的形式）。 如需詳細資訊，請參閱 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。 如果在呼叫此函數時，系統資訊中沒有任何專案，則函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDataSource**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效或為 Null。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求* 失敗|安裝程式無法執行 *fRequest* 引數所要求的作業。 對 **ConfigDSN** 的呼叫失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或翻譯工具安裝程式庫|無法載入驅動程式安裝程式程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDataSource** 會使用 *lpszDriver* 的值，從系統資訊讀取驅動程式安裝程式 DLL 的完整路徑。 它會載入 DLL，並使用傳遞給它的相同引數來呼叫 **ConfigDSN** 。  
  
 如果找不到或無法載入安裝 DLL 或使用者取消對話方塊， **SQLConfigDataSource**會傳回 FALSE。 否則，它會傳回從 **ConfigDSN**收到的狀態。  
  
 **SQLConfigDataSource** 會將系統 dsn *FRequest*對應至使用者 dsn *fRequest*s (ODBC_ADD_SYS_DSN ODBC_ADD_DSN、ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN，以及 ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DSN) 。 為了區分使用者和系統 Dsn， **SQLConfigDataSource** 會根據下表設定安裝程式設定模式。 在傳回之前， **SQLConfigDataSource** 會將設定模式重設為 BOTHDSN。 **ConfigDSN** (由驅動程式所執行) 應該呼叫 **SQLWriteDSNToIni** 和 **SQLWritePrivateProfileString** 來支援系統 DSN。 如需詳細資訊，請參閱 [ConfigDSN 函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*fRequest*|設定模式|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|安裝 DLL 中的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) () |  
|從系統資訊中移除資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|將資料來源名稱加入系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
