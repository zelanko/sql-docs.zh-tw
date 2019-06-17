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
manager: craigg
ms.openlocfilehash: 59b5cae9075d9d3c692d56e74edebabda8884fe2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537585"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 函數 (英文)
**合規性**  
 導入的版本：ODBC 1.0  
  
 **摘要**  
 **SQLConfigDataSource**新增、 修改或刪除資料來源。  
  
 功能**SQLConfigDataSource**也可以使用存取[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
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
 [輸入]父視窗控制代碼。 如果控制代碼為 null，函式不會顯示任何對話方塊。  
  
 *fRequest*  
 [輸入]要求的類型。 *常見*引數必須包含下列值之一：  
  
 ODBC_ADD_DSN:加入新的使用者資料來源。  
  
 ODBC_CONFIG_DSN:設定 （修改） 現有的使用者資料來源。  
  
 ODBC_REMOVE_DSN:移除現有的使用者資料來源。  
  
 ODBC_ADD_SYS_DSN:加入新的系統資料來源。  
  
 ODBC_CONFIG_SYS_DSN:修改現有的系統資料來源。  
  
 ODBC_REMOVE_SYS_DSN:移除現有的系統資料來源。  
  
 ODBC_REMOVE_DEFAULT_DSN:移除系統資訊中的預設資料來源規格 」 一節。 （它也會移除預設的驅動程式規格區段 Odbcinst.ini 中的項目系統資訊。 這*常見*執行相同的功能已被取代**SQLRemoveDefaultDataSource**函式。)指定此選項時，所有的呼叫中的其他參數**SQLConfigDataSource**應該是 Null; 如果不是 NULL，則會忽略它們。  
  
 *lpszDriver*  
 [輸入]驅動程式描述 （通常是相關聯的 DBMS 的名稱） 呈現給使用者，而不是實體的驅動程式名稱。  
  
 *lpszAttributes*  
 [輸入]雙向的 null 終止的關鍵字-值配對的形式的屬性清單。 如需詳細資訊，請參閱 < [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。 如果系統資訊 中的項目不存在，此函式呼叫時，此函式會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDataSource**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數是無效或為 NULL。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*常見*引數不是下列其中之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszDriver*引數無效。 它找不到在登錄中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行要求的作業*常見*引數。 若要在呼叫**ConfigDSN**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯器的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDataSource**會使用值*lpszDriver*讀取系統資訊的驅動程式安裝程式 DLL 的完整路徑。 它會載入 DLL 呼叫**ConfigDSN**使用相同的引數已傳遞給它。  
  
 **SQLConfigDataSource**如果無法找到或載入安裝程式 DLL，或如果使用者取消 [] 對話方塊中，會傳回 FALSE。 否則，它會傳回它收到的狀態**ConfigDSN**。  
  
 **SQLConfigDataSource**對應系統 DSN*常見*至 使用者 DSN*常見*s (ODBC_ADD_SYS_DSN 至 ODBC_ADD_DSN、 ODBC_CONFIG_DSN，和 ODBC_REMOVE_SYS_ ODBC_CONFIG_SYS_DSNDSN 來 ODBC_REMOVE_DSN)。 為了區分使用者與系統 Dsn **SQLConfigDataSource**設定安裝程式，根據下表的組態模式。 傳回前, **SQLConfigDataSource**將組態模式重設 BOTHDSN。 **ConfigDSN** （實作驅動程式） 應該呼叫**SQLWriteDSNToIni**並**SQLWritePrivateProfileString**支援系統 DSN。 如需詳細資訊，請參閱 < [ConfigDSN 函式](../../../odbc/reference/syntax/configdsn-function.md)。  
  
|*fRequest*|設定模式|  
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
|將資料來源名稱新增至 系統資訊|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
