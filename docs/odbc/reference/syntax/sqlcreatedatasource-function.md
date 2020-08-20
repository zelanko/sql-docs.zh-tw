---
description: SQLCreateDataSource 函式
title: SQLCreateDataSource 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb65e0906e7b69666dd04824f9c4d0819837d2b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461210"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函式
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLCreateDataSource** 會顯示對話方塊，讓使用者可以在其中加入資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd*  
 輸出父視窗控制碼。  
  
 *lpszDS*  
 輸出資料來源名稱。 *lpszDS* 可以是 null 指標或空字串。  
  
## <a name="returns"></a>傳回  
 如果已建立資料來源， **SQLCreateDataSource**會傳回 TRUE。 否則，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCreateDataSource**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*Hwnd*引數無效或為 Null。|  
|ODBC_ERROR_INVALID_DSN|不正確 DSN|*LpszDS*引數包含對 DSN 不正確字串。|  
|ODBC_ERROR_REQUEST_FAILED|*要求* 失敗|使用 ODBC_ADD_DSN 選項的 **ConfigDSN** 呼叫失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或翻譯工具安裝程式庫|無法載入驅動程式安裝程式程式庫。|  
|ODBC_ERROR_USER_CANCELED|使用者取消的作業|使用者已取消建立新的資料來源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|無法建立要求的 DSN|無法連接到資料庫;檔案 DSN 的 **SQLDriverConnect** 呼叫未傳回成功的連接。<br /><br /> 無法寫入檔案。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 如果 *hwnd* 為 null，則 **SQLCREATEDATASOURCE** 會傳回 FALSE。 否則，它會顯示 [ **建立新資料來源** ] 對話方塊，其中包含用來選擇要設定之資料來源類型的 wizard 頁面，如下圖所示。  
  
 ![建立新資料來源對話方塊：選取型別](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 預設選項是檔案 **資料來源**。 選擇資料來源並按一下 **[下一步** ] 時，會顯示包含已安裝驅動程式清單的下列 wizard 頁面。  
  
 ![建立新資料來源對話方塊：選取驅動程式](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果按一下 [ **取消** ]，對話方塊就會消失，且 **SQLCreateDataSource** 會傳回錯誤，錯誤碼為 ODBC_ERROR_USER_CANCELED。 如果選取了 [ **使用者資料來源** ] 或 [ **系統資料來源** ] 選項，[ **Advanced** ] 按鈕便無法使用。  
  
 按一下 [ **下一步]** 按鈕時，會發生下列其中一種情況，視所選取的資料來源類型而定：  
  
-   如果選取了 [檔案 **資料來源** ]，則會顯示一個嚮導頁面，讓使用者輸入檔案名。  
  
-   如果選取了 [ **使用者資料來源** ] 或 [ **系統資料來源** ]，則會顯示會顯示資料來源和驅動程式類型的 wizard 頁面以供審查，而且按一下 **[完成]** 時，就會設定資料來源。  
  
 如果從 [建立新的資料來源嚮導] 頁面按一下 [ **Advanced** ]，則會顯示一個嚮導頁面，讓使用者輸入驅動程式特定的資訊。 在此對話方塊的文字方塊中，輸入以傳用方式分隔的驅動程式和關鍵字，如下圖所示。  
  
 ![[進階檔案 DSN 建立設定] 對話方塊](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 您可以在 **SQLDriverConnect**的描述下找到其他的驅動程式特定關鍵字。 允許所有除外的 **DSN** 。  
  
 [ **驗證此連接** ] 選項的預設值為 TRUE。 此預設值適用於是否啟用此 wizard 頁面。 如果按一下 **[確定]** ，則會快取文字方塊中指定的字串和 [ **確認此連接** 選項] 值。  (如果按一下 [ **關閉** ] 按鈕或 [ **取消** ]，則會遺失任何新輸入的驅動程式特定資訊，因為文字方塊中指定的字串和 [ **驗證此連接** 選項] 值都不會快取。 )   
  
 如果在第一個嚮導頁面中選取了 [檔案 **資料來源** ]，則在選取驅動程式並在 [Advanced wizard] 頁面中輸入關鍵字值之後，系統會提示使用者輸入檔案名。 按一下 **[流覽]** 以搜尋檔案名，在這種情況下， **流覽** 方塊中的預設目錄是透過 HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion 和 "ODBC\DataSources" 中 CommonFileDir 指定的路徑組合來指定。  (如果 CommonFileDir 是 "C:\Program Files\Common Files"，預設目錄會是 "C:\Program Files\Common Files\ODBC\Data 來源"。 )   
  
 當您輸入檔案名，然後按一下 **[下一步]** 時，會針對作業系統的標準檔案命名規則檢查輸入的檔案名是否有效。 如果檔案名無效，會出現錯誤訊息框，通知使用者輸入了不正確檔案名。 當使用者確認訊息框之後，焦點會回到 [wizard] 頁面，其中輸入的檔案名。 如果檔案名有效，則會顯示會顯示所選關鍵字-值組的 wizard 頁面，如下圖所示。  
  
 ![建立新資料來源對話方塊：檢閱](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果按一下 **[完成]** ，並選取 [檔案**資料來源**] 做為資料來源類型，而且如果 [**驗證此連接**] 選項為 [TRUE]，則會使用**SAVEFILE**和**驅動程式**關鍵字來呼叫**SQLDriverConnect** 。 *DriverCompletion*引數設定為 SQL_DRIVER_COMPLETE。 **SAVEFILE**關鍵字的檔案名是輸入或選擇的名稱，而**driver**關鍵字的驅動程式名稱是所選擇的名稱。 如果 [Advanced wizard] 頁面中已指定驅動程式特定的連接字串，則該字串會附加在 **driver** 關鍵字之後。  
  
 如果 **SQLDriverConnect** 傳回 SQL_SUCCESS，驅動程式管理員就會建立 File DSN。 **SQLCreateDataSource** 會傳回 TRUE。 如果 **SQLDriverConnect** 未傳回 SQL_SUCCESS，則會出現警告訊息框，指出無法連接到資料來源。 仍然可以建立具有基本連接資訊的 DSN。 此訊息方塊可讓使用者取消或繼續建立 File DSN。  
  
 如果使用者選擇繼續建立 DSN，此程式會繼續執行，就像 **驗證此** 連線選項設定為 FALSE 一樣。 如果使用者選擇取消，則會針對 **SQLCreateDataSource** 傳回 FALSE，錯誤碼為 ODBC_ERROR_CREATE_DSN_FAILED。  
  
 如果選取 [檔案 **資料來源** ] 做為資料來源類型，而且 [ **驗證此連接** ] 選項為 [FALSE]，則會使用 **驅動程式** 關鍵字和使用者指定的連接字串來建立檔案 DSN (如果有任何來自 [Advanced wizard] 頁面的) 。 如果檔案建立成功， **SQLCreateDataSource**會傳回 TRUE。 如果檔案建立失敗，會出現錯誤訊息框，通知使用者作業系統傳回了任何錯誤。 針對 **SQLCreateDataSource** 傳回 FALSE，錯誤碼為 ODBC_ERROR_CREATE_DSN_FAILED。 如需檔案資料來源的詳細資訊，請參閱 [使用檔案資料來源進行連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或參閱 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果選取 [**使用者**] 或 [**系統資料來源**] 做為資料來源類型，則會使用 ODBC_ADD_DSN *fRequest*呼叫驅動程式安裝程式庫中的**ConfigDSN** 。 如需詳細資訊，請參閱 [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|管理資料來源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
