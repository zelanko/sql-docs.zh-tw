---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3a6fced096c779b5ab91bf4e5b6a3f0a66e5f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68121392"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函式
**標準**  
 引進的版本： ODBC 2。0  
  
 **摘要**  
 **SQLCreateDataSource**會顯示一個對話方塊，使用者可以在其中新增資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd*  
 源父視窗控制碼。  
  
 *lpszDS*  
 源資料來源名稱。 *lpszDS*可以是 null 指標或空字串。  
  
## <a name="returns"></a>傳回值  
 如果建立資料來源， **SQLCreateDataSource**會傳回 TRUE。 否則，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCreateDataSource**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*Hwnd*引數無效或為 Null。|  
|ODBC_ERROR_INVALID_DSN|不正確 DSN|*LpszDS*引數包含對 DSN 不正確字串。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|使用 ODBC_ADD_DSN 選項呼叫**ConfigDSN**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或 translator 安裝程式程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_USER_CANCELED|使用者已取消作業|使用者已取消建立新的資料來源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|無法建立要求的 DSN|無法連接到資料庫;檔案 DSN 的**SQLDriverConnect**呼叫未傳回成功的連接。<br /><br /> 無法寫入檔案。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 如果*hwnd*為 Null， **SQLCREATEDATASOURCE**會傳回 FALSE。 否則，它會顯示 [**建立新的資料來源**] 對話方塊，其中包含用來選擇要設定之資料來源類型的 wizard 頁面，如下圖所示。  
  
 ![建立新資料來源對話方塊：選取型別](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 預設選項為 [檔案**資料來源**]。 當您選擇資料來源並按一下**下一步**時，會顯示包含已安裝驅動程式清單的下列 wizard 頁面。  
  
 ![建立新資料來源對話方塊：選取驅動程式](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果按一下 [**取消**]，對話方塊就會消失，而**SQLCREATEDATASOURCE**會傳回 FALSE，錯誤碼為 ODBC_ERROR_USER_CANCELED。 如果已選取 [**使用者資料來源**] 或 [**系統資料來源**] 選項，[ **Advanced** ] 按鈕就無法使用。  
  
 按一下 [**下一步]** 按鈕時，將會發生下列其中一種情況，視選取的資料來源類型而定：  
  
-   如果已選取 [檔案**資料來源**]，則會顯示 [wizard] 頁面，供使用者輸入檔案名。  
  
-   如果選取了 [**使用者資料來源**] 或 [**系統資料來源**]，則會顯示顯示資料來源和驅動程式類型的 wizard 頁面進行審核，而當您按一下 **[完成]** 時，就會設定資料來源。  
  
 如果按一下 [建立新的資料來源嚮導] 頁面中的 [ **Advanced** ]，則會顯示 [wizard] 頁面，讓使用者輸入驅動程式特定的資訊。 在此對話方塊的文字方塊中，輸入以傳回分隔的驅動程式和關鍵字，如下圖所示。  
  
 ![[進階檔案 DSN 建立設定] 對話方塊](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 您可以在**SQLDriverConnect**的 [描述] 下找到其他的驅動程式特定關鍵字。 除了**DSN**以外，所有的都是允許的。  
  
 [**驗證此連接**] 選項的預設值為 TRUE。 此預設值適用於是否啟用此 wizard 頁面。 如果按一下 **[確定]** ，則會快取文字方塊中指定的字串和 [**確認此連接**選項] 值。 （如果按一下 [**關閉**] 按鈕或 [**取消**]，任何新輸入的驅動程式特定資訊都會遺失，因為文字方塊中指定的字串和 [**確認此連接**選項] 值不會被快取）。  
  
 如果在第一個 [wizard] 頁面中選取了 [檔案**資料來源**]，則在選取驅動程式並于 [Advanced wizard] 頁面中輸入關鍵字值之後，系統會提示使用者輸入檔案名。 按一下 **[流覽]** 以搜尋檔案名，在此情況下，[**流覽]** 方塊中的預設目錄是由 HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion 和 "ODBC\DataSources" 中 CommonFileDir 所指定的路徑組合來指定。 （如果 CommonFileDir 是 "C:\Program Files\Common Files"，則預設目錄會是 "C:\Program Files\Common Files\ODBC\Data 來源"）。  
  
 輸入檔案名，然後按一下 **[下一步]** 時，系統會檢查輸入的檔案名是否符合作業系統的標準檔案命名規則的有效性。 如果檔案名無效，則會出現錯誤訊息框，通知使用者輸入的檔案名無效。 在使用者認可訊息方塊之後，焦點就會回到 [wizard] 頁面，其中會輸入檔案名。 如果檔案名有效，則會顯示 [wizard] 頁面，顯示所選取的關鍵字-值組以供審查，如下圖所示。  
  
 ![建立新資料來源對話方塊：檢閱](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果按一下 **[完成]** ，並選取 [檔案**資料來源**] 做為資料來源類型，而且如果 [**確認此連接**] 選項為 TRUE，則會使用**SAVEFILE**和**驅動程式**關鍵字來呼叫**SQLDriverConnect** 。 *DriverCompletion*引數設定為 SQL_DRIVER_COMPLETE。 **SAVEFILE**關鍵字的檔案名是輸入或選擇的名稱，**驅動程式**關鍵字的驅動程式名稱是所選擇的名稱。 如果在 [Advanced wizard] 頁面中指定了驅動程式特定的連接字串，該字串就會附加在**driver**關鍵字之後。  
  
 如果**SQLDriverConnect**傳回 SQL_SUCCESS，驅動程式管理員就會建立檔案 DSN。 **SQLCreateDataSource**會傳回 TRUE。 如果**SQLDriverConnect**未傳回 SQL_SUCCESS，就會出現警告訊息框，指出無法連接到資料來源。 仍然可以建立具有最少連接資訊的 DSN。 此訊息方塊可讓使用者取消或繼續建立檔案 DSN。  
  
 如果使用者選擇繼續建立 DSN，此程式會繼續進行，如同 [**確認此連接**] 選項設定為 [FALSE]。 如果使用者選擇取消，則會針對**SQLCreateDataSource**傳回 FALSE，錯誤碼為 ODBC_ERROR_CREATE_DSN_FAILED。  
  
 如果選取 [檔案**資料來源**] 做為 [資料來源類型]，而 [**確認此連接**選項] 為 [FALSE]，則會使用 [Advanced wizard] 頁面中的 [**驅動程式**] 關鍵字和 [使用者指定的連接字串（如果有的話）] 來建立檔案 DSN。 如果檔案建立成功，則會針對**SQLCreateDataSource**傳回 TRUE。 如果檔案建立不成功，則會出現錯誤訊息框，通知使用者作業系統傳回了任何錯誤。 針對**SQLCreateDataSource**傳回 FALSE，錯誤碼為 ODBC_ERROR_CREATE_DSN_FAILED。 如需有關檔案資料來源的詳細資訊，請參閱[使用檔案資料來源連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果已選取 [**使用者**] 或 [**系統資料來源**] 做為資料來源類型，則會使用 ODBC_ADD_DSN *fRequest*來呼叫驅動程式安裝程式庫中的**ConfigDSN** 。 如需詳細資訊，請參閱[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|管理資料來源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
