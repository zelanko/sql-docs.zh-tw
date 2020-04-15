---
title: SQL建立資料來源函數 |微軟文件
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
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301198"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLCreateDataSource**顯示一個對話框,使用者可以使用該對話框添加數據源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引數  
 *霍恩德*  
 [輸入]父視窗句柄。  
  
 *lpszDS*  
 [輸入]數據源名稱。 *lpszDS*可以是空指標或空字串。  
  
## <a name="returns"></a>傳回值  
 如果創建了資料源 **,SQLCreateDataSource**將返回 TRUE。 否則,它將返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCreateDataSource**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式碼*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd*參數無效或 NULL。|  
|ODBC_ERROR_INVALID_DSN|不合法的 DSN|*lpszDS*參數包含一個對 DSN 無效的字串。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|使用ODBC_ADD_DSN選項對**ConfigDSN**的呼叫失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉換器設定庫|無法載入驅動程式設置庫。|  
|ODBC_ERROR_USER_CANCELED|使用者取消的作業|使用者取消了創建新數據源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|無法建立要求的 DSN|無法連接到資料庫;對**SQLDriverConnect**的檔案 DSN 的呼叫未傳回成功的連線。<br /><br /> 無法寫入檔。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 如果*hwnd*為空 **,SQLCreate 數據源**將返回 FALSE。 否則,它將顯示 **「創建新資料源**」對話框,其中包含用於選擇要設置的數據源類型的嚮導頁,如下圖所示。  
  
 ![建立新資料來源對話方塊：選取型別](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 預設選項是**檔案資料來源**。 選擇數據源並按**下 Next**後,將顯示以下包含已安裝驅動程式清單的嚮導頁。  
  
 ![建立新資料來源對話方塊：選取驅動程式](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果按下 **「取消」** 對話方塊將消失 **,SQLCreateDataSource**將 FALSE 傳回,錯誤代碼為 ODBC_ERROR_USER_CANCELED。 如果選擇了 **「使用者資料來源**」或 **「系統資料源」** 選項,則 **「進階**」按鈕不可用。  
  
 按下 **「 下一步**」按鈕時,將發生以下情況之一,具體取決於選擇了哪種類型的數據來源:  
  
-   如果選擇了**文件數據源**,則將顯示一個嚮導頁,供使用者輸入檔名。  
  
-   如果選擇了 **「使用者資料來源**」 或 **「系統資料來源**」,將顯示顯示資料源類型和驅動程式的精靈頁進行審閱,按一下 **「完成」** 時,將設定資料來源。  
  
 如果從"創建新資料來源"向導頁按下 **「高級」** 則將顯示一個精靈頁,供使用者輸入特定於驅動程式的資訊。 在此對話框的文字框中,鍵入驅動程式和關鍵字以返回分隔,如下圖所示。  
  
 ![[進階檔案 DSN 建立設定] 對話方塊](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 其他特定於驅動程式的關鍵字可以在**SQLDriverConnect**的描述中找到。 除**DSN**外,所有內容均允許。  
  
 **'驗證此連線**'選項的預設值為 TRUE。 無論是否啟動此嚮導頁,此預設值都適用。 如果按下 **「確定」** 則快取文字框中指定的字串和 **「驗證此連線」** 選項值。 (如果按下「**關閉**」 按鈕或 **「取消」** 則新輸入的任何特定於驅動程式的資訊都會遺失,因為文字框中指定的字串和 **「驗證此連接」** 選項值不會緩存。  
  
 如果在第一個嚮導頁中選擇了**文件數據源**,則在選擇驅動程式並在高級嚮導頁中輸入關鍵字值后,系統將提示使用者輸入檔名。 按下 **「瀏覽」** 以搜尋檔案名,在這種情況下,「**瀏覽」** 框中的預設目錄由 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Microsoft_Windows_CurrentVersion 和「ODBC_資料來源」中的常見檔案 Dir 指定的路徑組合指定。 (如果 CommonFileDir 是"C:*程式檔\公共檔",則默認目錄為"C:程式檔\常見檔\ODBC_資料來源"。  
  
 輸入檔名並按**下 Next**後,將對照作業系統的標準檔案命名規則檢查輸入的檔名的有效性。 如果檔名無效,則錯誤消息框會通知使用者已輸入無效的檔名。 使用者確認消息框後,焦點將返回到輸入檔名的嚮導頁。 如果檔名有效,將顯示顯示所選關鍵字值對的嚮導頁供審閱,如下圖所示。  
  
 ![建立新資料來源對話方塊：檢閱](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果按下 **「完成」** 並選擇**檔案資料來源**為資料源類型,並且 **「驗證此連線**」 選項為 TRUE",則使用 **「儲存檔案」** 和 **「驅動程式」** 關鍵字呼叫**SQLDriverConnect。** *驅動程式完成*參數設置為SQL_DRIVER_COMPLETE。 **SAVEFILE**關鍵字的檔名是輸入或選擇的名稱 **,DRIVER**關鍵字的驅動程式名稱是所選的名稱。 如果在進階精靈中指定特定於驅動程式的連接字串,則該字串將追加到**DRIVER**關鍵字之後。  
  
 如果**SQLDriverConnect**傳回SQL_SUCCESS,驅動程式管理員已創建檔案 DSN。 **SQLCreate數據源**傳回 TRUE。 如果**SQLDriverConnect**未返回SQL_SUCCESS,則警告消息框指示無法與數據源建立連接。 仍可創建具有最少連接資訊的 DSN。 此消息框允許使用者取消或繼續創建檔案 DSN。  
  
 如果用戶選擇繼續創建 DSN,此過程將繼續,就像**驗證此連接**選項設置為 FALSE 一樣。 如果用戶選擇取消,則為**SQLCreateDataSource**返回 FALSE,錯誤代碼為ODBC_ERROR_CREATE_DSN_FAILED。  
  
 如果選擇**檔案資料來源**為資料來源類型,並且 **「驗證此連線**」選項為 FALSE,則使用**DRIVER**關鍵字創建檔案 DSN,並從進階精靈創建使用者指定的連接字串(如果有)。 如果檔案建立成功,則傳回 TRUE 以**SQLCreateDataSource**。 如果文件創建不成功,則錯誤消息框會通知使用者從作業系統返回的任何錯誤。 為**SQLCreateDataSource**傳回 FALSE,錯誤代碼為ODBC_ERROR_CREATE_DSN_FAILED。 關於檔案資料來源的詳細資訊,請參考[使用檔案資料來源連線](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 或請參考[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果選擇**使用者**或**系統數據來源**作為資料來源類型,則使用ODBC_ADD_DSN *fRequest*調用驅動程式設置庫中的**ConfigDSN。** 有關詳細資訊,請參閱[設定DSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|管理資料來源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
