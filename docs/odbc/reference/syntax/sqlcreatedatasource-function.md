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
manager: craigg
ms.openlocfilehash: 8b432e8d40952574f1264e07a0b09e91a1e334b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537606"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函式
**合規性**  
 導入的版本：ODBC 2.0  
  
 **摘要**  
 **SQLCreateDataSource**顯示的對話方塊，使用者可以加入資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd*  
 [輸入]父視窗控制代碼。  
  
 *lpszDS*  
 [輸入]資料來源名稱。 *lpszDS*可以是 null 指標或空字串。  
  
## <a name="returns"></a>傳回值  
 **SQLCreateDataSource**會傳回 TRUE，如果在建立資料來源。 否則，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCreateDataSource**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*Hwnd*引數是無效或為 NULL。|  
|ODBC_ERROR_INVALID_DSN|無效的資料來源名稱|*LpszDS*引數包含無效的資料來源名稱的字串。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|若要在呼叫**ConfigDSN** ODBC_ADD_DSN 選項失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯器的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_USER_CANCELED|使用者已取消作業|使用者已取消建立新的資料來源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|無法建立要求的資料來源名稱|無法連接到資料庫，例如：若要在呼叫**SQLDriverConnect**的檔案 DSN 未傳回成功的連線。<br /><br /> 無法寫入檔案。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 如果*hwnd*為 null，然後**SQLCreateDataSource**會傳回 FALSE。 否則，它會顯示**建立新的資料來源** 精靈頁面，選擇要設定好之後，資料來源的類型，如下圖所示的對話方塊。  
  
 ![建立新的資料來源對話方塊： 選取型別](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 預設選項是**檔案的資料來源**。 當資料來源已被選擇並**下一步**按下，會顯示下列精靈頁面，其中包含一份已安裝的驅動程式。  
  
 ![建立新的資料來源對話方塊： 選取的驅動程式](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果**取消**按一下時，對話方塊方塊就會消失並**SQLCreateDataSource** ODBC_ERROR_USER_CANCELED 錯誤碼傳回 FALSE。 如果有任一**使用者資料來源**或**系統資料來源**選取選項，則**進階**按鈕便無法使用。  
  
 當**下一步**按一下按鈕時，將會發生下列其中一種，視哪一種資料來源已選取：  
  
-   如果**檔案的資料來源**已選取，精靈頁面會顯示使用者輸入檔案名稱。  
  
-   如果有任一**使用者資料來源**或**系統資料來源**已選取，顯示的資料來源及驅動程式類型的精靈頁面會顯示供檢閱，和當**完成**是按下，資料來源設定。  
  
 如果**進階**按下 [建立新的資料來源精靈] 頁面上，從一個精靈頁面會顯示使用者輸入驅動程式特有的資訊。 在此對話方塊的文字方塊中，輸入驅動程式和關鍵字分隔傳回，如下圖所示。  
  
 ![進階檔案 DSN 建立設定 對話方塊](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 描述您可以找到額外的驅動程式專屬關鍵字**SQLDriverConnect**。 以外的所有**DSN**允許。  
  
 預設值**確認此連線**選項為 TRUE。 已啟動此精靈頁面，則會套用此預設值。 如果 **[確定]** 按一下時，在文字方塊中指定的字串與**確認這個連線**快取選項值。 (如果**關閉** 按鈕或**取消**按一下時，任何新輸入驅動程式專屬資訊都會遺失，因為在文字方塊中指定的字串和**確認這個連線**不會快取選項值。)  
  
 如果**檔案的資料來源**選取在第一個精靈頁面中，然後選取 驅動程式，並已在 進階 精靈頁面中輸入關鍵字值之後，系統會提示使用者輸入檔案名稱。 按一下 **瀏覽**檔案名稱時，請在此情況下預設目錄中的搜尋**瀏覽**方塊由在 HKEY_LOCAL_MACHINE\SOFTWARE\ CommonFileDir 所指定之路徑的組合Microsoft\Windows\CurrentVersion 和 「 ODBC\DataSources"。 （如果 CommonFileDir"C:\Program Files\Common Files"，預設目錄會是"C:\Program Files\Common Files\ODBC\Data 來源 >。）  
  
 當輸入檔案名稱和**下一步**按一下時，檔案會檢查輸入的名稱，對作業系統的標準檔案命名規則的有效性。 如果檔案名稱無效，錯誤訊息方塊會通知使用者，輸入檔案名稱無效。 使用者確認訊息方塊之後，焦點會回到精靈頁面中輸入檔案名稱。 如果檔案名稱是有效的會顯示精靈頁面，其中顯示所選的關鍵字-值配對供檢閱，如下圖所示。  
  
 ![建立新的資料來源對話方塊： 檢閱](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果**完成**按下並**檔案資料來源**做為資料來源類型中，選取如果**確認此連線**選項為 TRUE， **SQLDriverConnect**以呼叫**SAVEFILE**並**驅動程式**關鍵字。 *DriverCompletion*引數設定為 SQL_DRIVER_COMPLETE。 檔案名稱，如**SAVEFILE**關鍵字是已輸入的名稱或選擇，而且驅動程式名稱**驅動程式**關鍵字是選擇的名稱。 如果在 [進階] 精靈頁面指定驅動程式特有的連接字串，該字串會附加後**驅動程式**關鍵字。  
  
 如果**SQLDriverConnect**傳回 SQL_SUCCESS，驅動程式管理員已建立檔案 DSN。 **SQLCreateDataSource** ，則傳回 TRUE。 如果**SQLDriverConnect**不會傳回 SQL_SUCCESS，一則警告訊息方塊表示，不會連接到資料來源。 仍可建立 DSN，以使用最少的連接資訊。 此訊息方塊可讓使用者取消或繼續進行檔案 DSN 建立作業。  
  
 如果使用者選擇繼續建立 DSN，繼續進行此程序一樣**確認此連線**選項已設定為 FALSE。 如果使用者選擇取消時，會傳回 FALSE **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED 錯誤碼。  
  
 如果**檔案資料來源**選為資料來源類型和**確認此連接**選項是 FALSE，會建立檔案 DSN**驅動程式**關鍵字和使用者指定連接字串 （如果有的話） 從 [進階] 精靈頁面。 如果檔案建立成功，則傳回 TRUE 的**SQLCreateDataSource**。 如果檔案建立不成功，錯誤訊息方塊會通知使用者從作業系統傳回任何錯誤。 會傳回 FALSE，如**SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED 錯誤碼。 如需檔案資料來源的詳細資訊，請參閱[連線使用的檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果**使用者**或是**系統資料來源**做為資料來源類型中，選取**ConfigDSN** ODBC_ADD_DSN 驅動程式安裝程式中呼叫程式庫*常見*。 如需詳細資訊，請參閱 < [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|管理資料來源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
