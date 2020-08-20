---
description: SQLManageDataSources
title: SQLManageDataSources |Microsoft Docs
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
ms.openlocfilehash: 81f4616cb04d5d17cca687843d28efa1027ff65f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460971"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLManageDataSources** 會顯示對話方塊，讓使用者可以在系統資訊中設定、新增和刪除資料來源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd*  
 輸出父視窗控制碼。  
  
## <a name="returns"></a>傳回  
 如果*hwnd*不是有效的視窗控制碼， **SQLMANAGEDATASOURCES**會傳回 FALSE。 否則就會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLManageDataSources**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求* 失敗|對 **ConfigDSN** 的呼叫失敗。|  
|ODBC_ERROR_INVALID__HWND|不正確視窗控制碼|*Hwnd*引數無效或為 Null。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="managing-data-sources"></a>管理資料來源  
 **SQLManageDataSources** 一開始會顯示 [ **ODBC 資料來源管理員** ] 對話方塊，如下圖所示。  
  
 ![[ODBC 資料來源管理員] 對話方塊](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 此對話方塊會顯示在下列三個索引標籤底下的系統資訊中所列出的資料來源： **使用者 DSN**、 **系統 DSN**和檔案 **DSN**。 如果使用者按兩下資料來源或選取資料來源，然後按一下 [ **設定**]， **SQLManageDataSources** 就會使用 ODBC_CONFIG_DSN 選項，在安裝 DLL 中呼叫 **ConfigDSN** 。  
  
 如果使用者按一下 [ **加入**]， **SQLManageDataSources** 會顯示 [ **建立新資料來源** ] 對話方塊，如下圖所示。  
  
 ![[建立新資料來源] 對話方塊：](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 對話方塊會顯示已安裝的驅動程式清單。 如果使用者按兩下驅動程式或選取驅動程式，然後按一下 **[確定]**， **SQLManageDataSources** 會在安裝程式 DLL 中呼叫 **ConfigDSN** ，並將它傳遞至 ODBC_ADD_DSN 選項。  
  
 如果使用者選取資料來源，然後按一下 [ **移除**]， **SQLManageDataSources** 會詢問使用者是否想要刪除資料來源。 如果使用者按一下 [ **是]**， **SQLManageDataSources** 會在安裝 DLL 中使用 ODBC_REMOVE_DSN 選項來呼叫 **ConfigDSN** 。  
  
 [ **建立新資料來源** ] 對話方塊是用來加入或刪除使用者資料來源、系統資料來源或檔案資料來源。  
  
## <a name="user-dsns"></a>使用者 Dsn  
 針對個別使用者所建立的 Dsn 將稱為「使用者 Dsn」，以區別它們與系統 Dsn。 系統資訊中的使用者 Dsn 註冊如下：  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系統 Dsn  
 [ **建立新資料來源** ] 對話方塊可讓您將系統資料來源新增至本機電腦或刪除一個，或設定系統資料來源的設定。  
  
 使用系統資料來源名稱設定的資料來源 (DSN) 可供同一部電腦上的多個使用者使用。 它也可以由全系統服務使用，即使沒有任何使用者登入電腦，也可以取得資料來源的存取權。  
  
 系統 DSN 會註冊在系統資訊的 HKEY_LOCAL_MACHINE 專案中，而不是在 HKEY_CURRENT_USER 專案中註冊。 它不會系結至一位登入其特定使用者名稱和密碼的使用者，但可供該電腦的任何使用者或自動全系統服務使用。 不過，系統 DSN 系結至一部電腦。 它不支援在電腦之間使用遠端 Dsn 的功能。 系統 Dsn 註冊的系統資訊如下：  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>檔案 Dsn  
 檔案資料來源沒有資料來源名稱，如同電腦資料來源，而且未註冊至任何一個使用者或電腦。 該資料來源的連接資訊會包含在可複製到任何電腦的 dsn 檔案中。 檔案資料來源可以是可共用的，在此情況下，當使用者已安裝適當的驅動程式時，該 dsn 檔案就會位於網路上，而且可供網路上的多個使用者同時使用。 檔案資料來源也可以是 unshareable 的，在這種情況下，它只能在單一電腦上使用。  
  
 如需檔案資料來源的詳細資訊，請參閱 [使用檔案資料來源進行連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或參閱 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驅動程式  
 如果使用者按一下 [ **ODBC 資料來源管理員**] 對話方塊中的 [**驅動程式**] 索引標籤， **SQLManageDataSources**會顯示安裝在系統上的 ODBC 驅動程式清單，以及驅動程式的相關資訊。 顯示的日期是驅動程式的建立日期，如下圖所示。  
  
 ![[ODBC 資料來源管理員] 的 [驅動程式] 索引標籤](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>追蹤選項  
 如果使用者按一下 [ **ODBC 資料來源管理員**] 對話方塊中的 [**追蹤**] 索引標籤， **SQLManageDataSources**會顯示追蹤選項，如下圖所示。  
  
 ![[ODBC 資料來源管理員] 的 [追蹤] 索引標籤](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果使用者按一下 [ **立即啟動追蹤** ]，然後按一下 **[確定]**， **SQLManageDataSources** 就會針對目前在電腦上執行的所有應用程式，手動啟用追蹤。  
  
 如果使用者在 [ **記錄檔路徑** ] 文字方塊中指定追蹤檔案的名稱，然後按一下 [ **確定]**， **SQLManageDataSources** 會在系統資訊的 [ODBC] 區段中，將 **TraceFile** 關鍵字設定為指定的名稱。  
  
> [!IMPORTANT]  
>  從 Windows 8 開始，Visual Studio Analyzer 的支援已移除 (Visual Studio Analyzer 僅包含在舊版的 Visual Studio ) 中。 如需替代的疑難排解機制，請使用「投標追蹤」。  
  
 如果使用者按一下 [ **開始] Visual Studio Analyzer** 然後按一下 **[確定]**，則 Visual Studio Analyzer 已啟用。 它會保持啟用狀態，直到按一下 [ **停止] Visual Studio Analyzer** 為止。  
  
 如需追蹤的詳細資訊，請參閱 [追蹤](../../../odbc/reference/develop-app/tracing.md)。 如需 **追蹤** 和 **TraceFile** 關鍵字的詳細資訊，請參閱 [ODBC](../../../odbc/reference/install/odbc-subkey.md)子機碼。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
