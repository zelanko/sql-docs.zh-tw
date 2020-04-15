---
title: SQL管理資料來源 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290212"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLManageDataSources**顯示一個對話框,使用者可以使用該對話框在系統資訊中設置、添加和刪除數據源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>引數  
 *霍恩德*  
 [輸入]父視窗句柄。  
  
## <a name="returns"></a>傳回值  
 如果*hwnd*不是有效的視窗句柄 **,SQLManageData 源**將返回 FALSE。 否則就會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLManageDataSources**返回 FALSE 時,可以通過調用**SQL 安裝程序獲取**關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|對**ConfigDSN 的**調用失敗。|  
|ODBC_ERROR_INVALID__HWND|無效的視窗句柄|*hwnd*參數無效或 NULL。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="managing-data-sources"></a>管理資料來源  
 **SQLManageDataSource**最初顯示**ODBC 數據來源管理員**對話框,如下圖所示。  
  
 ![[ODBC 資料來源管理員] 對話方塊](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 這個對話框在三個選項卡下顯示系統資訊中列出的資料來源:**使用者 DSN,** 系統**DSN**和**檔案 DSN**。 如果使用者雙擊資料源或選擇資料來源並按下設定**Configure****「,SQLManageDataSource**在設定 DLL 中呼叫**ConfigDSN,** 並帶有ODBC_CONFIG_DSN選項。  
  
 如果使用者按下「**添加** **」,SQLManageDataSources**將顯示 **「創建新資料來源」** 對話框,如下圖所示。  
  
 ![[建立新資料來源] 對話方塊：](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 該對話框顯示已安裝驅動程式的清單。 如果用戶雙擊驅動程式或選擇驅動程式並按**下 「確定****」,SQLManageDataSources**在設置 DLL 中調用**ConfigDSN**並傳遞ODBC_ADD_DSN選項。  
  
 如果使用者選擇數據源並按下 **「刪除****」,SQLManageDataSource**會詢問使用者是否要刪除數據來源。 如果使用者按下「**是****」,SQLManageDataSources**在設定 DLL 中呼叫**ConfigDSN,** 並帶有ODBC_REMOVE_DSN選項。  
  
 **"建立新資料來源'** 對話框用於新增或刪除使用者資料源、系統資料源或檔案資料來源。  
  
## <a name="user-dsns"></a>使用者 DSN  
 為單個使用者創建的 DSN 將稱為使用者 DSN,以將其與系統 DSN 區分開來。 使用者 DSN 在系統資訊中註冊如下:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系統 DSN  
 **"建立新資料源'** 對話方塊允許您向本地電腦添加系統資料源或刪除一個,或設定系統資料源的配置。  
  
 使用系統數據源名稱 (DSN) 設置的數據源可以由同一台電腦上的多個使用者使用。 它也可以由系統範圍的服務使用,然後即使沒有用戶登錄到計算機,該服務也可以訪問數據源。  
  
 系統 DSN 在系統資訊HKEY_LOCAL_MACHINE條目中註冊,而不是在HKEY_CURRENT_USER條目中註冊。 它不綁定到使用其特定使用者名和密碼登錄的使用者,但該電腦的任何使用者或自動系統範圍的服務都可以使用。 但是,系統DSN與一台電腦綁定。 它不支援在計算機之間使用遠端 DSN 的功能。 系統 DSN 在系統資訊中註冊如下:  
  
 HKEY_LOCAL_MACHINE軟體 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>檔案 DSN  
 檔資料來源沒有資料來源名稱,電腦數據來源也是如此,並且不註冊給任何一個使用者或電腦。 該資料來源的連接資訊包含在可以複製到任何電腦的 .dsn 檔中。 檔數據源可以共用,在這種情況下,.dsn 檔駐留在網路上,並且只要使用者安裝了適當的驅動程式,就可以由網路上的多個使用者同時使用。 檔數據源也可以不可共用,在這種情況下,它只能在一台電腦上使用。  
  
 關於檔案資料來源的詳細資訊,請參考[使用檔案資料來源連線](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), 或請參考[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驅動程式  
 如果使用者按下**ODBC 資料來源管理員**對話方塊中的 **「驅動程式」** 選項卡 **,SQLManageDataSource**將顯示系統上安裝的 ODBC 驅動程式的清單以及有關驅動程式的資訊。 顯示的日期是驅動程式的創建日期,如下圖所示。  
  
 ![[ODBC 資料來源管理員] 的 [驅動程式] 索引標籤](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>追蹤選項  
 如果使用者按下**ODBC 資料來源管理員**對話方塊中的 **「追蹤」** 選項卡 **,SQLManageDataSources**將顯示追蹤選項,如下圖所示。  
  
 ![[ODBC 資料來源管理員] 的 [追蹤] 索引標籤](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果使用者按下「**立即開始追蹤」 ,** 然後按下 **「 確定****」,SQLManageDataSources**可手動追蹤電腦上目前執行的所有應用程式。  
  
 如果使用者在**日誌檔 Path**文本框中指定追蹤檔的名稱,然後單擊 **「確定****」,SQLManageDataSources**將系統資訊 [ODBC] 部分中的**TraceFile**關鍵字設置為指定的名稱。  
  
> [!IMPORTANT]  
>  從 Windows 8 開始刪除了對可視化工作室分析器的支援(視覺工作室分析器僅包含在舊版本的 Visual Studio 中)。 對於其他故障排除機制,請使用 BID 跟蹤。  
  
 如果用戶按下「**開始視覺工作室分析器**」,然後單擊「**確定**」,則啟用了可視化工作室分析器。 在單擊**停止可視化工作室分析器**之前,它將保持啟用狀態。  
  
 有關追蹤的詳細資訊,請參閱[追蹤](../../../odbc/reference/develop-app/tracing.md)。 有關**追蹤**與**追蹤檔案**關鍵字的詳細資訊,請參閱[ODBC 子鍵](../../../odbc/reference/install/odbc-subkey.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreate資料來源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
