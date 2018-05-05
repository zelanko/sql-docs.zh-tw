---
title: SQLConfigDataSource 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddff49350de9d4e713b065848ab53649b25cb094
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 函數 (英文)
**一致性**  
 版本引進了： ODBC 1.0  
  
 **摘要**  
 **SQLConfigDataSource**新增、 修改或刪除資料來源。  
  
 功能**SQLConfigDataSource**也可以使用存取[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 [輸入]父視窗控制代碼。 如果控制代碼為 null，函式不會顯示任何對話方塊。  
  
 *常見*  
 [輸入]要求的類型。 *常見*引數必須包含下列值之一：  
  
 ODBC_ADD_DSN： 加入新的使用者資料來源。  
  
 ODBC_CONFIG_DSN： 設定 （修改） 現有的使用者資料來源。  
  
 ODBC_REMOVE_DSN： 移除現有的使用者資料來源。  
  
 ODBC_ADD_SYS_DSN： 加入新的系統資料來源。  
  
 ODBC_CONFIG_SYS_DSN： 修改現有的系統資料來源。  
  
 ODBC_REMOVE_SYS_DSN： 移除現有的系統資料來源。  
  
 ODBC_REMOVE_DEFAULT_DSN： 移除的系統資訊的預設資料來源規格 > 一節。 （它也會移除預設驅動程式規格區段 Odbcinst.ini 項目中的系統資訊。 這*常見*執行相同的功能已被取代**SQLRemoveDefaultDataSource**函式。)當指定這個選項時，所有的呼叫中的其他參數**SQLConfigDataSource**應該是 Null; 如果不是 NULL，則會忽略它們。  
  
 *lpszDriver*  
 [輸入]驅動程式說明 （通常是相關聯的 DBMS 名稱） 呈現給使用者，而不是實體的驅動程式名稱。  
  
 *lpszAttributes*  
 [輸入]雙向的 null 終止的關鍵字-值組表單中的屬性清單。 如需詳細資訊，請參閱[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊的項目不存在，此函式呼叫時，函數會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDataSource**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數以前是無效或為 NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*常見*引數不是下列其中之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。 它不在登錄中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行所要求的操作*常見*引數。 若要呼叫**ConfigDSN**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯程式的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDataSource**會使用值*lpszDriver*讀取系統資訊的驅動程式安裝 DLL 的完整路徑。 它會載入 DLL 呼叫**ConfigDSN**與已傳遞給它的相同引數。  
  
 **SQLConfigDataSource**如果找不到或載入 DLL 的安裝，或使用者取消對話方塊會傳回 FALSE。 否則，它會傳回它收到來自狀態**ConfigDSN**。  
  
 **SQLConfigDataSource**對應系統 DSN*常見*使用者 DSN 的 s*常見*s 至 ODBC_ADD_DSN (ODBC_ADD_SYS_DSN、 ODBC_CONFIG_DSN，和 ODBC_REMOVE_SYS_ ODBC_CONFIG_SYS_DSNDSN ODBC_REMOVE_DSN)。 為了區分使用者和系統 Dsn **SQLConfigDataSource**設定安裝程式，根據下表的組態模式。 在傳回時之前, **SQLConfigDataSource** BOTHDSN 重設為組態模式。 **ConfigDSN** （實作由驅動程式） 應該呼叫**SQLWriteDSNToIni**和**SQLWritePrivateProfileString**支援系統 DSN。 如需詳細資訊，請參閱[ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*常見*|設定模式|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安裝程式 DLL 中）|  
|移除系統資訊的資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|加入系統資訊的資料來源名稱|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
