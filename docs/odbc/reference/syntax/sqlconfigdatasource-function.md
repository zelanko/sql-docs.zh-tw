---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7706d3a7dd05273b4608d49211a6eaab8927f2a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118611"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 函數 (英文)
**標準**  
 引進的版本： ODBC 1。0  
  
 **摘要**  
 **SQLConfigDataSource**加入、修改或刪除資料來源。  
  
 您也可以使用 ODBCCONF 來存取**SQLConfigDataSource**的功能[。EXE](../../../odbc/odbcconf-exe.md)。  
  
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
 源父視窗控制碼。 如果控制碼為 null，函數不會顯示任何對話方塊。  
  
 *fRequest*  
 源要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_ADD_DSN：加入新的使用者資料來源。  
  
 ODBC_CONFIG_DSN：設定（修改）現有的使用者資料來源。  
  
 ODBC_REMOVE_DSN：移除現有的使用者資料來源。  
  
 ODBC_ADD_SYS_DSN：加入新的系統資料來源。  
  
 ODBC_CONFIG_SYS_DSN：修改現有的系統資料來源。  
  
 ODBC_REMOVE_SYS_DSN：移除現有的系統資料來源。  
  
 ODBC_REMOVE_DEFAULT_DSN：移除系統資訊中的預設資料來源規格區段。 （它也會移除系統資訊中 Odbcinst 專案的預設驅動程式規格區段。 這個*fRequest*會執行與已被取代的**SQLRemoveDefaultDataSource**函式相同的功能）。當指定這個選項時，呼叫**SQLConfigDataSource**的所有其他參數都應該是 null。如果它們不是 Null，則會忽略它們。  
  
 *lpszDriver*  
 源驅動程式描述（通常是相關 DBMS 的名稱）會呈現給使用者，而不是實體驅動程式名稱。  
  
 *lpszAttributes*  
 源成對的雙向 null 終止屬性清單，其格式為關鍵字-值組。 如需詳細資訊，請參閱[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。 如果在呼叫此函式時，系統資訊中沒有任何專案存在，此函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDataSource**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效或為 Null。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行*fRequest*引數所要求的作業。 呼叫**ConfigDSN**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或 translator 安裝程式程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDataSource**會使用*lpszDriver*的值，從系統資訊讀取驅動程式安裝程式 DLL 的完整路徑。 它會載入 DLL，並使用傳遞給它的相同引數呼叫**ConfigDSN** 。  
  
 如果**SQLConfigDataSource**找不到或無法載入安裝程式 DLL，或使用者取消了對話方塊，則會傳回 FALSE。 否則，它會傳回從**ConfigDSN**收到的狀態。  
  
 **SQLConfigDataSource**會將系統 dsn *FRequest*對應到使用者 dsn *fRequest*s （ODBC_ADD_SYS_DSN 以 ODBC_ADD_DSN、ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN，以及 ODBC_REMOVE_SYS_DSN 至 ODBC_REMOVE_DSN）。 為了區分使用者和系統 Dsn， **SQLConfigDataSource**會根據下表來設定安裝程式設定模式。 在傳回之前， **SQLConfigDataSource**會將設定模式重設為 BOTHDSN。 **ConfigDSN** （由驅動程式執行）應該呼叫**SQLWriteDSNToIni**和**SQLWritePrivateProfileString**來支援系統 DSN。 如需詳細資訊，請參閱[ConfigDSN 函數](../../../odbc/reference/syntax/configdsn-function.md)。  
  
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
|加入、修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安裝程式 DLL 中）|  
|從系統資訊移除資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|將資料來源名稱新增至系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
