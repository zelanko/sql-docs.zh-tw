---
title: 設定DSN功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbae126c819088bd277621b207454503a86c8955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306039"
---
# <a name="configdsn-function"></a>ConfigDSN 函式
**一致性**  
 版本介紹: ODBC 1.0  
  
 **摘要**  
 **配置DSN**添加、修改或刪除系統資訊中的數據源。 它可能會提示使用者提供連接資訊。 它可以在驅動程式 DLL 或單獨的設置 DLL 中。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd 家長*  
 [輸入]父視窗句柄。 如果句柄為空,則函數將不會顯示任何對話方塊。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*參數必須包含以下值之一:  
  
 ODBC_ADD_DSN:添加新數據源。  
  
 ODBC_CONFIG_DSN:配置(修改)現有數據源。  
  
 ODBC_REMOVE_DSN:刪除現有數據源。  
  
 *lpszDriver*  
 [輸入]向使用者而不是物理驅動程式名稱顯示的驅動程式描述(通常是關聯的 DBMS 的名稱)。  
  
 *lpsz屬性*  
 [輸入]以關鍵字-值對形式加倍終止的屬性清單。 有關詳細資訊,請參閱"註釋"。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDSN**傳回 FALSE 時,透過呼叫**SQLPost 安裝程式錯誤**將關聯的*\*pfError 程式*碼值發布到安裝程式錯誤緩衝區,並且可以透過呼叫**SQL 安裝程式錯誤**獲得。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效關鍵字-值對|*lpszAttributes*參數包含語法錯誤。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。 在註冊表中找不到它。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_ADD_DSNODBC_CONFIG_DSNODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行*fRequest*參數請求的操作。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或轉換器特定錯誤|驅動程式特定的錯誤,沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPost 安裝程式錯誤**函數時 *,SzError*參數應包含特定於驅動程式的錯誤訊息。|  
  
## <a name="comments"></a>註解  
 **ConfigDSN**從安裝程式 DLL 接收連接資訊,作為關鍵字-值對形式的屬性清單。 每個對都用空位元組終止,整個清單用空位元組終止。 (即,兩個空位元組標記清單的末尾。關鍵字值對中的等號周圍不允許空格。 **配置DSN**可以接受不是**SQLBrowseConnect**和**SQLDriverConnect**的有效關鍵字。 **設定DSN**不一定支援所有關鍵字,是有效的關鍵字**的SQLBrowse連接**與**SQLDriver 連接**。 (**配置DSN**不接受**DRIVER**關鍵字。**ConfigDSN**函數使用的關鍵字必須支援使用安裝程式的 AUTO 設定功能重新建立資料來源所需的所有選項。 當**ConfigDSN**值和連接字串值的使用相同時,應使用相同的關鍵字。  
  
 與**SQLBrowseConnect**和**SQLDriverConnect**中一樣,關鍵字及其值不應包含 ***("";??{}\**!]** 字元和**DSN**關鍵字的值不能僅包含空白。 由於註冊表語法,關鍵字和數據源名稱不能包含反斜杠\\( ) 字元。  
  
 **ConfigDSN**應呼叫**SQLValidDSN**來檢查資料來源名稱的長度,並驗證名稱中是否不包含無效字元。 如果數據源名稱長於SQL_MAX_DSN_LENGTH或包含無效字元 **,SQLValidDSN**將返回錯誤 **,ConfigDSN**將返回錯誤。 **SQLWriteDSNToIni**也檢查數據源名稱的長度。  
  
 例如,要設定需要使用者 ID、密碼和資料庫名稱的資料來源,安裝程式可能會傳遞以下關鍵字-值對:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 有關這些關鍵字的詳細資訊,請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每個驅動程式的文檔。  
  
 要顯示對話框 *,hwndParent*不能為空。  
  
## <a name="adding-a-data-source"></a>加入資料來源  
 如果資料來源名稱在*lpszAttributes*中傳遞到**ConfigDSN,****則 ConfigDSN**將檢查該名稱是否有效。 如果數據源名稱與現有數據源名稱匹配,並且*hwndParent*為 null,**則 ConfigDSN**將覆蓋現有名稱。 如果它與現有名稱匹配,並且*hwndParent*不為空 **,ConfigDSN**會提示用戶覆蓋現有名稱。  
  
 如果*lpszAttributes*包含足夠的資訊以連接到資料來源 **,ConfigDSN**可以添加資料來源或顯示一個對話框,使用者可以使用該對話框更改連接資訊。 如果 lpszAttributes 不包含足夠的資訊以連接到數據來源,ConfigDSN 必須確定必要的資訊;如果*lpszAttributes*沒有包含足夠的資訊來連接到數據源。因此 **,ConfigDSN**必須確定必要的資訊。如果*hwndParent*不為空,則顯示一個對話方塊,用於從使用者中檢索資訊。  
  
 如果**ConfigDSN**顯示一個對話框,它必須在*lpszAttributes*中顯示傳遞給它的任何連接資訊。 特別是,如果數據源名稱傳遞給它 **,ConfigDSN**將顯示該名稱,但不允許使用者更改該名稱。 **ConfigDSN**可以為未在*lpszAttributes*中傳遞給它的連接資訊提供預設值。  
  
 如果**ConfigDSN**無法取得數據來源的完整連接資訊,它將傳回 FALSE。  
  
 如果**ConfigDSN**可以取得資料來源的完整連接資訊,它將在安裝程式 DLL 中呼叫**SQLWriteDSNToini**以將新的資料來源規範添加到 Odbc.ini 檔案(或註冊表)。 **SQLWriteDSNToI**將資料源名稱添加到 [ODBC 資料來源] 部分,創建資料來源規範部分,並將**DRIVER**關鍵字與驅動程式描述作為其值。 **配置DSN**在安裝程式 DLL 中調用**SQLWritePrivateProfileString**來添加驅動程式使用的任何其他關鍵字和值。  
  
## <a name="modifying-a-data-source"></a>變更資料來源  
 要修改數據源,必須在*lpszAttributes*中將數據源名稱傳遞給**ConfigDSN。** **配置DSN**檢查資料來源名稱是否位於Odbc.ini檔(或註冊表)中。  
  
 如果*hwndParent*為空 **,ConfigDSN**將使用*lpszAttributes*中的資訊來修改 Odbc.ini 檔(或註冊表)中的資訊。 如果*hwndParent*不是 null,**則 ConfigDSN**將顯示一個對話框,使用*lpszAttributes*中的資訊;對於不在*lpszAttributes*中的資訊,它使用來自系統資訊的資訊。 用戶可以在**ConfigDSN**將其儲存在系統資訊之前對其進行修改。  
  
 如果資料來源名稱已更改 **,ConfigDSN**首先在安裝程式 DLL 中呼叫**SQLRemoveDSNFromIni,** 以從 Odbc.ini 檔案(或註冊表)中刪除現有的資料來源規範。 然後,按照上一節中的步驟添加新的數據源規範。 如果未更改資料源名稱 **,ConfigDSN**在安裝程式 DLL 中調用**SQLWritePrivateProfileString**進行任何其他更改。 **配置DSN**不得刪除或更改**驅動程式**關鍵字的值。  
  
## <a name="deleting-a-data-source"></a>刪除資料來源  
 要刪除資料源,必須在*lpszAttributes*中將數據源名稱傳遞給**ConfigDSN。** **配置DSN**檢查資料來源名稱是否位於Odbc.ini檔(或註冊表)中。 然後,它會在安裝程式 DLL 中調用**SQLRemoveDSN Fromini**以刪除數據來源。  
  
## <a name="note"></a>附註
 如果編寫此例程的 Unicode 版本,則必須將其稱為**ConfigDSNW,** 使用 LPCWSTR 參數而不是 LPCSTR。
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|從 Odbc.ini 檔案或註冊表取得值|[SQLGet 私人設定檔字串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|移除預設資料來源|[SQL 移除預設資料來源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|從 Odbc.ini(或註冊表)中移除資料來源名稱|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|將資料來源名稱加入 Odbc.ini(或註冊表)|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|將值寫入 Odbc.ini 檔案或註冊表|[SQLWrite 私有設定檔字串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
