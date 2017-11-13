---
title: "SQLManageDataSources |Microsoft 文件"
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
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8785fef25830aa3987470a8007e115da1cc73a42
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLManageDataSources**會顯示一個對話方塊，使用者可以設定、 新增和刪除資料來源中的系統資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd*  
 [輸入]父視窗控制代碼。  
  
## <a name="returns"></a>傳回值  
 **SQLManageDataSources**則傳回 FALSE *hwnd*不是有效的視窗控制代碼。 否則，它會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLManageDataSources**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|若要呼叫**ConfigDSN**失敗。|  
|ODBC_ERROR_INVALID__HWND|無效的視窗控制代碼|*Hwnd*引數以前是無效或為 NULL。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="managing-data-sources"></a>管理資料來源  
 **SQLManageDataSources**一開始會顯示**ODBC 資料來源管理員**對話方塊中，在下圖所示。  
  
 ![ODBC 資料來源管理員 對話方塊](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 對話方塊會顯示三個索引標籤下的系統資訊中所列的資料來源：**使用者 DSN**，**系統 DSN**，和**檔案 DSN**。 如果使用者按兩下資料來源或選取資料來源並按一下**設定**， **SQLManageDataSources**呼叫**ConfigDSN**在安裝程式中使用 ODBC_CONFIG_ DLLDSN 選項。  
  
 如果使用者按一下**新增**， **SQLManageDataSources**顯示**建立新的資料來源**對話方塊中，如下圖所示。  
  
 ![建立新的資料來源 對話方塊](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 對話方塊會顯示已安裝的驅動程式清單。 如果使用者按兩下驅動程式或驅動程式會選取並按一下**確定**， **SQLManageDataSources**呼叫**ConfigDSN**中安裝 DLL 並將其傳遞 ODBC_ADD_DSN 選項。  
  
 如果使用者可以選取資料來源，並按一下**移除**， **SQLManageDataSources**詢問使用者是否要刪除資料來源。 如果使用者按一下**是**， **SQLManageDataSources**呼叫**ConfigDSN**在安裝程式 DLL 中使用 ODBC_REMOVE_DSN 選項。  
  
 **建立新的資料來源**對話方塊用來加入或刪除使用者資料來源、 系統資料來源或檔案資料來源。  
  
## <a name="user-dsns"></a>使用者名稱 （dsn)  
 建立針對個別使用者的名稱 （dsn） 會呼叫使用者 Dsn，以便區別系統 Dsn。 使用者 Dsn 中的系統資訊註冊，如下所示：  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系統 Dsn  
 **建立新的資料來源**對話方塊可讓您可將系統資料來源加入至您的本機電腦或刪除其中一個，或設定系統資料來源的組態。  
  
 設定系統資料來源名稱 (DSN) 的資料來源可供多個使用者在相同電腦上。 它也可以使用全系統服務，然後取得資料來源的存取，即使沒有任何使用者登入電腦。  
  
 系統 DSN 會註冊在 HKEY_LOCAL_MACHINE 項目中的系統資訊，而不是在 HKEY_CURRENT_USER 項目。 它不會連結到一個使用者使用他或她特定的使用者名稱和密碼登入，但是可以使用該電腦的任何使用者或自動的全系統服務。 系統 DSN，不過，繫結到一部電腦。 不支援使用遠端電腦之間的 Dsn 的功能。 系統 Dsn 中的系統資訊註冊，如下所示：  
  
 HKEY_LOCAL_MACHINE 軟體 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>檔案 Dsn  
 檔案資料來源沒有資料來源名稱，不會機器資料來源，以及未登錄至任何一個使用者或電腦。 該資料來源的連接資訊包含在可以複製到任何機器.dsn 檔案。 檔案資料來源可以是可共用，在此情況下.dsn 檔案位於網路，並可以同時使用多個網路上的使用者，只要使用者擁有適當的驅動程式安裝。 檔案資料來源也可以是非共用，如此只有單一機器上使用。  
  
 如需有關檔案資料來源的詳細資訊，請參閱[連接使用的檔案資料來源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驅動程式  
 如果使用者按一下**驅動程式**索引標籤中**ODBC 資料來源管理員**對話方塊中， **SQLManageDataSources**顯示在系統上，安裝 ODBC 驅動程式的清單以及驅動程式的相關資訊。 在下圖所示，顯示的日期會是驅動程式的建立日期。  
  
 ![ODBC 資料來源管理員驅動程式 索引標籤](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>追蹤選項  
 如果使用者按一下**追蹤**索引標籤中**ODBC 資料來源管理員**對話方塊中， **SQLManageDataSources**顯示追蹤選項，如下列所示圖例。  
  
 ![ODBC 資料來源管理員追蹤 索引標籤](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果使用者按一下**立即開始追蹤**然後按一下 **確定**， **SQLManageDataSources**啟用手動追蹤目前在電腦上執行的所有應用程式。  
  
 如果使用者指定追蹤檔案中的檔案名稱**記錄檔路徑**文字方塊中，然後按一下**確定**， **SQLManageDataSources**設定**TraceFile**為指定之名稱的系統資訊 [ODBC] 區段中的關鍵字。  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer 的支援已移除開頭 （Visual Studio Analyzer 只包含在舊版的 Visual Studio）。 Windows 8 中。 如需疑難排解機制的替代方法，使用 BID 追蹤。  
  
 如果使用者按一下**啟動 Visual Studio Analyzer** ，然後按一下**確定**，Visual Studio Analyzer 已啟用。 它會維持啟用狀態直到**停止 Visual Studio Analyzer**按下。  
  
 如需有關追蹤的詳細資訊，請參閱[追蹤](../../../odbc/reference/develop-app/tracing.md)。 如需有關**追蹤**和**TraceFile**關鍵字，請參閱[ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|

