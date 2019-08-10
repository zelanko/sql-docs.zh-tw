---
title: ConfigDSN 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21a02107359b26c0dc30aa87acbf46c1ab1a172d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892857"
---
# <a name="configdsn-function"></a>ConfigDSN 函式
**標準**  
 引進的版本:ODBC 1。0  
  
 **摘要**  
 **ConfigDSN**會新增、修改或刪除系統資訊中的資料來源。 它可能會提示使用者輸入連接資訊。 它可以位於驅動程式 DLL 或個別的安裝程式 DLL 中。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 源父視窗控制碼。 如果控制碼為 null, 函數不會顯示任何對話方塊。  
  
 *fRequest*  
 源要求的類型。 *FRequest*引數必須包含下列其中一個值:  
  
 ODBC_ADD_DSN:加入新的資料來源。  
  
 ODBC_CONFIG_DSN:設定 (修改) 現有的資料來源。  
  
 ODBC_REMOVE_DSN:移除現有的資料來源。  
  
 *lpszDriver*  
 源驅動程式描述 (通常是相關 DBMS 的名稱) 會呈現給使用者, 而不是實體驅動程式名稱。  
  
 *lpszAttributes*  
 源成對的雙向 null 終止屬性清單, 其格式為關鍵字-值組。 如需詳細資訊, 請參閱「批註」。  
  
## <a name="returns"></a>傳回值  
 如果成功, 函式會傳回 TRUE, 如果失敗, 則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDSN**傳回 FALSE 時, 會 *\** 呼叫**SQLPostInstallerError**來將相關聯的 pfErrorCode 值張貼到安裝程式錯誤緩衝區, 並可透過呼叫**SQLInstallerError**來取得。 下表列出可由**SQLInstallerError**傳回的 *\*pfErrorCode*值, 並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行*fRequest*引數所要求的作業。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或 translator 特定的錯誤|驅動程式特定的錯誤, 其中沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPostInstallerError**函式中的*SzError*引數應該包含驅動程式特定的錯誤訊息。|  
  
## <a name="comments"></a>註解  
 **ConfigDSN**會從安裝程式 DLL 接收連接資訊, 做為關鍵字-值組格式的屬性清單。 每個配對都會以 null 位元組結束, 而整個清單會以 null 位元組結束。 (也就是兩個 null 位元組會標示清單結尾)。關鍵字-值組的等號前後不能有空格。 **ConfigDSN**可以接受對**SQLBrowseConnect**和**SQLDriverConnect**而言無效關鍵字的關鍵字。 **ConfigDSN**不一定支援**SQLBrowseConnect**和**SQLDriverConnect**的有效關鍵字的所有關鍵詞。 (**ConfigDSN**不接受**DRIVER**關鍵字)。**ConfigDSN**函數所使用的關鍵字必須支援使用安裝程式的自動安裝功能來重新建立資料來源所需的所有選項。 當使用**ConfigDSN**值且連接字串值相同時, 應該使用相同的關鍵字。  
  
 如同在**SQLBrowseConnect**和**SQLDriverConnect**中, 關鍵字和其值不應包含 **[]{}()、;？=\*! @** 字元, 而**DSN**關鍵字的值不能只包含空格。 由於登錄文法的原因, 關鍵字和資料來源名稱不能包含反斜線\\() 字元。  
  
 **ConfigDSN**應該呼叫**SQLValidDSN**以檢查資料來源名稱的長度, 並確認名稱中沒有包含不正確字元。 如果資料來源名稱的長度超過 SQL_MAX_DSN_LENGTH 或包含不正確字元, **SQLValidDSN**會傳回錯誤, 而**ConfigDSN**會傳回錯誤。 **SQLWriteDSNToIni**也會檢查資料來源名稱的長度。  
  
 例如, 若要設定需要使用者識別碼、密碼和資料庫名稱的資料來源, 安裝應用程式可能會傳遞下列關鍵字-值組:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 如需這些關鍵字的詳細資訊, 請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每個驅動程式的檔。  
  
 若要顯示對話方塊, *hwndParent*不得為 null。  
  
## <a name="adding-a-data-source"></a>加入資料來源  
 如果將資料來源名稱傳遞至*lpszAttributes*中的**ConfigDSN** , 則**ConfigDSN**會檢查名稱是否有效。 如果資料來源名稱符合現有的資料來源名稱, 而且*hwndParent*為 null, 則**ConfigDSN**會覆寫現有的名稱。 如果它符合現有的名稱, 而*hwndParent*不是 null, 則**ConfigDSN**會提示使用者覆寫現有的名稱。  
  
 如果*lpszAttributes*包含足夠的資訊可連接到資料來源, **ConfigDSN**可以新增資料來源或顯示對話方塊, 使用者可以在其中變更連接資訊。 如果*lpszAttributes*未包含足夠的資訊來連接到資料來源, **ConfigDSN**必須判斷必要的資訊。如果*hwndParent*不是 null, 它會顯示一個對話方塊, 以從中抓取使用者的資訊。  
  
 如果**ConfigDSN**顯示對話方塊, 它就必須在*lpszAttributes*中顯示傳遞給它的任何連接資訊。 特別是, 如果資料來源名稱已傳遞給它, **ConfigDSN**會顯示該名稱, 但不允許使用者變更它。 **ConfigDSN**可以針對未在*lpszAttributes*中傳遞的連接資訊提供預設值。  
  
 如果**ConfigDSN**無法取得資料來源的完整連接資訊, 它會傳回 FALSE。  
  
 如果**ConfigDSN**可以取得資料來源的完整連接資訊, 它會在安裝程式 DLL 中呼叫**SQLWriteDSNToIni** , 以將新的資料來源規格加入至 Odbc .ini 檔案 (或登錄)。 **SQLWriteDSNToIni**會將資料來源名稱新增至 [ODBC 資料來源] 區段、建立資料來源規格區段, 並加入**驅動**程式關鍵字與驅動程式描述作為其值。 **ConfigDSN**會呼叫安裝程式 DLL 中的**SQLWritePrivateProfileString** , 以新增驅動程式所使用的任何其他關鍵字和值。  
  
## <a name="modifying-a-data-source"></a>修改資料來源  
 若要修改資料來源, 必須將資料來源名稱傳遞至*lpszAttributes*中的**ConfigDSN** 。 **ConfigDSN**會檢查資料來源名稱是否在 Odbc .ini 檔案中 (或登錄)。  
  
 如果*hwndParent*為 Null, **ConfigDSN**會使用*lpszAttributes*中的資訊來修改 Odbc .ini 檔案 (或登錄) 中的資訊。 如果*hwndParent*不是 Null, **ConfigDSN**會使用*lpszAttributes*中的資訊來顯示對話方塊。對於不在*lpszAttributes*中的資訊, 它會使用系統資訊中的資訊。 在**ConfigDSN**將資訊儲存在系統資訊之前, 使用者可以修改該資訊。  
  
 如果資料來源名稱已變更, **ConfigDSN**會先呼叫安裝程式 DLL 中的**SQLRemoveDSNFromIni** , 以從 Odbc .ini 檔案 (或登錄) 中移除現有的資料來源規格。 接著, 它會遵循上一節中的步驟來新增資料來源規格。 如果資料來源名稱未變更, **ConfigDSN**會呼叫安裝程式 DLL 中的**SQLWritePrivateProfileString** , 以進行其他任何變更。 **ConfigDSN**不能刪除或變更**Driver**關鍵字的值。  
  
## <a name="deleting-a-data-source"></a>刪除資料來源  
 若要刪除資料來源, 必須將資料來源名稱傳遞至*lpszAttributes*中的**ConfigDSN** 。 **ConfigDSN**會檢查資料來源名稱是否在 Odbc .ini 檔案中 (或登錄)。 然後, 它會在安裝程式 DLL 中呼叫**SQLRemoveDSNFromIni** , 以移除資料來源。  
  
## <a name="note"></a>附註
 如果撰寫此常式的 Unicode 版本, 則必須使用 LPCWSTR 引數 (而非 LPCSTR) 呼叫**ConfigDSNW**。
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|加入、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|從 Odbc .ini 檔案或登錄取得值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|移除預設資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|從 Odbc .ini (或登錄) 移除資料來源名稱|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|將資料來源名稱新增至 Odbc .ini (或登錄)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|將值寫入至 Odbc .ini 檔案或登錄|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
