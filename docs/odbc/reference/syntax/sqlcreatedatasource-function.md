---
title: "SQLCreateDataSource 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c4c7b0b4ebecf75f1bcf31b0b1716a7076513488
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函式
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLCreateDataSource**顯示的對話方塊，可用的使用者可以加入資料來源。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 **SQLCreateDataSource**傳回 TRUE，如果在建立資料來源。 否則，它會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCreateDataSource**傳回 FALSE，相關聯* \*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出* \*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*Hwnd*引數以前是無效或為 NULL。|  
|ODBC_ERROR_INVALID_DSN|無效的資料來源名稱|*LpszDS*引數包含無效的資料來源名稱的字串。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|若要呼叫**ConfigDSN** ODBC_ADD_DSN 選項失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯程式的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_USER_CANCELED|使用者已取消作業|使用者已取消建立新的資料來源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|無法建立要求的資料來源名稱|無法連接到資料庫。若要呼叫**SQLDriverConnect**針對檔案 DSN 未傳回成功的連接。<br /><br /> 無法寫入檔案。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 如果*hwnd*為 null， **SQLCreateDataSource**會傳回 FALSE。 否則，它會顯示**建立新的資料來源**與精靈頁面選擇要設定好之後，資料來源類型，如下圖所示的對話方塊。  
  
 ![建立新的資料來源對話方塊： 選取型別](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 預設選項是**檔案資料來源**。 當已被選擇資料來源和**下一步**按下，會顯示下列精靈頁面中，其中包含已安裝的驅動程式清單。  
  
 ![建立新的資料來源對話方塊： 選取的驅動程式](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果**取消**按一下時，對話方塊方塊就會消失， **SQLCreateDataSource** ODBC_ERROR_USER_CANCELED 錯誤碼會傳回 FALSE。 如果有任一個**使用者資料來源**或**系統資料來源**選取選項，則**進階**按鈕便無法使用。  
  
 當**下一步**按一下按鈕時，將會發生下列其中一個、 來源所依據的資料類型選取：  
  
-   如果**檔案資料來源**已選取，精靈頁面會顯示使用者輸入檔案名稱。  
  
-   如果有任一個**使用者資料來源**或**系統資料來源**已選取，顯示的資料來源及驅動程式類型的精靈頁面會顯示供檢閱，以及當**完成**是按一下資料來源設定。  
  
 如果**進階**按下 建立新的資料來源精靈頁面上，從一個精靈頁面會顯示使用者輸入驅動程式特有的資訊。 在此對話方塊的文字方塊中，輸入驅動程式和關鍵字以傳回，分隔下圖所示。  
  
 ![進階檔案 DSN 建立設定 對話方塊](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 描述您可以找到其他驅動程式特有的關鍵字**SQLDriverConnect**。 除了**DSN**允許。  
  
 預設值為**確認此連接**選項為 TRUE。 不論是否已啟動此精靈頁面，適用於此預設值。 如果**確定**按一下時，在文字方塊中指定的字串和**確認此連接**會快取選項值。 (如果**關閉**按鈕或**取消**按一下時，任何新輸入驅動程式特定資訊都會遺失，因為在文字方塊中指定的字串和**確認此連接**選項值不會快取。)  
  
 如果**檔案資料來源**選取驅動程式，並且已在進階的精靈頁面中輸入關鍵字值之後，提示使用者輸入的檔案名稱，然後在第一個精靈頁面中，選取。 按一下**瀏覽**來搜尋檔案名稱，在這種情況中的預設目錄**瀏覽**方塊指定 CommonFileDir HKEY_LOCAL_MACHINE\SOFTWARE\ 中所指定之路徑的組合Microsoft\Windows\CurrentVersion 和 「 ODBC\DataSources"。 （如果 CommonFileDir"C:\Program Files\Common Files"，預設目錄是 「 C:\Program Files\Common Files\ODBC\Data 來源 」。）  
  
 當已輸入檔案名稱和**下一步**按一下時，檔案會檢查對作業系統的標準檔案命名規則的有效輸入名稱。 如果檔案名稱無效，錯誤訊息方塊通知使用者已輸入了無效的檔案名稱。 在使用者確認收到的訊息方塊之後，焦點會傳回到精靈頁面中輸入檔案名稱。 如果檔案名稱是有效的會顯示精靈頁面，其中顯示所選的關鍵字-值組供檢閱下, 圖所示。  
  
 ![建立新的資料來源對話方塊： 檢閱](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果**完成**按一下和**檔案資料來源**做為資料來源類型中，選取如果**確認此連接**選項為 TRUE， **SQLDriverConnect**呼叫**SAVEFILE**和**驅動程式**關鍵字。 *DriverCompletion*引數設定為 SQL_DRIVER_COMPLETE。 檔案名稱**SAVEFILE**關鍵字是已輸入的名稱或選擇，且驅動程式名稱**驅動程式**關鍵字是已選擇的名稱。 如果在進階的精靈頁面中指定驅動程式特有的連接字串，該字串會附加後**驅動程式**關鍵字。  
  
 如果**SQLDriverConnect**傳回 SQL_SUCCESS，驅動程式管理員已建立 檔案 DSN。 **SQLCreateDataSource** ，則傳回 TRUE。 如果**SQLDriverConnect**不會傳回 SQL_SUCCESS，警告訊息方塊會指出不可能資料來源建立連接。 仍會建立使用最少的連接資訊的 DSN。 此訊息方塊可讓使用者可以取消，或檔案 DSN 建立繼續執行。  
  
 如果使用者選擇要繼續建立 DSN，此程序會繼續如同**確認此連接**選項已設定為 FALSE。 如果使用者選擇取消時，會傳回 FALSE **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED 錯誤碼。  
  
 如果**檔案資料來源**選取做為資料來源類型和**確認此連接**選項是 FALSE，檔案 DSN 會透過**驅動程式**關鍵字和使用者指定進階的精靈頁面，從連接字串 （如果有的話）。 如果檔案建立成功，則傳回 TRUE 的**SQLCreateDataSource**。 如果檔案建立不成功，錯誤訊息方塊通知使用者從作業系統傳回任何錯誤。 會傳回 FALSE **SQLCreateDataSource** ODBC_ERROR_CREATE_DSN_FAILED 錯誤碼。 如需檔案資料來源的詳細資訊，請參閱[連接使用的檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果**使用者**或**系統資料來源**做為資料來源類型中，選取**ConfigDSN** ODBC_ADD_DSN 驅動程式安裝程式中呼叫程式庫*常見*。 如需詳細資訊，請參閱[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|管理資料來源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|

