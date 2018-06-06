---
title: ConfigDSN 函式 |Microsoft 文件
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
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8b75fb1b87a4f6199999e5d5e33d8cd0083bac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configdsn-function"></a>ConfigDSN 函式
**一致性**  
 版本引進了： ODBC 1.0  
  
 **摘要**  
 **ConfigDSN**新增、 修改或刪除資料來源的系統資訊。 它可能會提示使用者輸入連接資訊。 它可以是驅動程式 DLL 或個別的安裝程式 DLL。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL ConfigDSN(  
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
  
 ODBC_ADD_DSN： 加入新的資料來源。  
  
 ODBC_CONFIG_DSN： 設定 （修改） 的現有資料來源。  
  
 ODBC_REMOVE_DSN： 移除現有的資料來源。  
  
 *lpszDriver*  
 [輸入]驅動程式說明 （通常是相關聯的 DBMS 名稱） 呈現給使用者，而不是實體的驅動程式名稱。  
  
 *lpszAttributes*  
 [輸入]雙向的 null 終止的關鍵字-值組表單中的屬性清單。 如需詳細資訊，請參閱 「 註解。 」  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDSN**傳回 FALSE，相關聯 *\*pfErrorCode*值由呼叫張貼至安裝程式錯誤緩衝區**SQLPostInstallerError**和可以藉由呼叫取得**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszAttributes*引數包含語法錯誤。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。 它不在登錄中。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*常見*引數不是下列其中之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行所要求的操作*常見*引數。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定驅動程式或轉譯器錯誤|驅動程式特有的錯誤，它沒有任何已定義的 ODBC 安裝程式發生錯誤。 *SzError*呼叫中的引數**SQLPostInstallerError**函式應該包含驅動程式特有的錯誤訊息。|  
  
## <a name="comments"></a>註解  
 **ConfigDSN**為關鍵字-值組表單中的屬性清單，安裝程式 DLL 的接收連接資訊。 每一對 null 位元組，以終止，並將整個清單終止 null 位元組。 （也就是兩個 null 位元組標記清單的結尾）。關鍵字-值配對中的等號前後不能有空格。 **ConfigDSN**可以接受關鍵字不是有效的關鍵字**SQLBrowseConnect**和**SQLDriverConnect**。 **ConfigDSN**並不一定支援所有的關鍵字是有效的關鍵字**SQLBrowseConnect**和**SQLDriverConnect**。 (**ConfigDSN**不接受**驅動程式**關鍵字。)所用的關鍵字**ConfigDSN**函式必須支援重新建立資料來源使用安裝程式的自動安裝程式功能所需的所有選項。 當使用**ConfigDSN**值和連接字串值相同，應該使用相同的關鍵字。  
  
 在**SQLBrowseConnect**和**SQLDriverConnect**，這些關鍵字，而且其值不應該包含 **[]{}（)，;？\*= ！ @** 字元和值**DSN**關鍵字不能只包含空格。 因為登錄文法中，關鍵字和資料來源名稱不能包含反斜線 (\\) 字元。  
  
 **ConfigDSN**應該呼叫**SQLValidDSN**以檢查資料來源名稱的長度，並驗證確定名稱中包含任何無效字元。 如果資料來源名稱長度超過 SQL_MAX_DSN_LENGTH 或包含無效的字元， **SQLValidDSN**會傳回錯誤和**ConfigDSN**會傳回錯誤。 也會檢查資料來源名稱的長度所**SQLWriteDSNToIni**。  
  
 例如，若要設定資料來源需要使用者識別碼、 密碼和資料庫名稱，安裝應用程式可能會傳遞下列關鍵字-值配對：  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 如需有關這些關鍵字的詳細資訊，請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每個驅動程式文件。  
  
 若要顯示對話方塊， *hwndParent*不得為 null。  
  
## <a name="adding-a-data-source"></a>加入資料來源  
 如果資料來源名稱傳遞至**ConfigDSN**中*lpszAttributes*， **ConfigDSN**檢查名稱是否有效。 如果資料來源名稱符合現有的資料來源名稱和*hwndParent*為 null， **ConfigDSN**會覆寫現有的名稱。 如果它符合現有的名稱和*hwndParent*不是 null， **ConfigDSN**會提示使用者覆寫現有的名稱。  
  
 如果*lpszAttributes*包含足夠的資訊來連接到資料來源， **ConfigDSN**可以加入資料來源，或顯示與使用者可以變更連接資訊的對話方塊。 如果*lpszAttributes*不包含足夠的資訊來連接到資料來源， **ConfigDSN**必須判斷所需的資訊; 如果*hwndParent*不是 null，它會顯示對話方塊，以從使用者擷取資訊。  
  
 如果**ConfigDSN**會顯示一個對話方塊，它必須顯示傳遞給它的任何連接資訊*lpszAttributes*。 特別是，如果資料來源名稱已傳遞給它， **ConfigDSN**顯示名稱，但不允許使用者變更它。 **ConfigDSN**可以提供預設值的連接資訊不會傳送到在*lpszAttributes*。  
  
 如果**ConfigDSN**無法取得完整的連線資訊的資料來源，它會傳回 FALSE。  
  
 如果**ConfigDSN**可以取得完整的連線資訊的資料來源，它會呼叫**SQLWriteDSNToIni** DLL 以加入新的資料來源規格 Odbc.ini 檔案 （或登錄） 的安裝程式中。 **SQLWriteDSNToIni** [ODBC 資料來源] 區段中加入資料來源名稱、 建立資料來源規格 > 一節，以及將**驅動程式**關鍵字搭配可做為其值的驅動程式描述。 **ConfigDSN**呼叫**SQLWritePrivateProfileString**在安裝程式 DLL 以加入任何其他關鍵字和驅動程式所使用的值。  
  
## <a name="modifying-a-data-source"></a>修改資料來源  
 若要修改資料來源，資料來源名稱必須傳遞給**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**檢查是否在 Odbc.ini 檔案 （或登錄） 的資料來源名稱。  
  
 如果*hwndParent*為 null， **ConfigDSN**使用中的資訊*lpszAttributes*修改中的 Odbc.ini 檔案 （或登錄） 的資訊。 如果*hwndParent*不是 null， **ConfigDSN**顯示使用中的資訊的對話方塊*lpszAttributes*; 資訊不能在*lpszAttributes*，它會使用來自 系統資訊的資訊。 使用者可以修改資訊再**ConfigDSN**將它儲存在系統資訊。  
  
 如果資料來源名稱已變更， **ConfigDSN**會先呼叫**SQLRemoveDSNFromIni**安裝程式中的 DLL，以便移除現有的資料來源從 Odbc.ini 檔案 （或登錄） 的規格。 然後，它會遵循上一節中新增新的資料來源規格中的步驟。 如果未變更的資料來源名稱， **ConfigDSN**呼叫**SQLWritePrivateProfileString**在安裝程式中的 DLL，以便進行任何其他變更。 **ConfigDSN**可能無法刪除或變更的值**驅動程式**關鍵字。  
  
## <a name="deleting-a-data-source"></a>刪除資料來源  
 若要刪除的資料來源，資料來源名稱必須傳遞給**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**檢查是否在 Odbc.ini 檔案 （或登錄） 的資料來源名稱。 然後它會呼叫**SQLRemoveDSNFromIni**在安裝程式中移除資料來源的 DLL。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|取得從 Odbc.ini 檔案或登錄值。|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|移除預設的資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|移除資料來源名稱從 Odbc.ini （或登錄）|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|將資料來源名稱加入至 Odbc.ini （或登錄）|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|寫入的 Odbc.ini 檔案或登錄值|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
