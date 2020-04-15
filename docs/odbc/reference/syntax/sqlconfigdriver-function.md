---
title: SQL 設定驅動程式功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301243"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函式
**一致性**  
 版本介紹: ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**載入相應的驅動程式設定 DLL 並調用**ConfigDriver**函數。  
  
 **SQLConfigDriver**的功能也可以與[ODBCCONF 一起訪問。EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd 家長*  
 [輸入]父視窗句柄。 如果句柄為空,則函數將不會顯示任何對話方塊。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*必須包含以下值之一:  
  
 ODBC_CONFIG_DRIVER:更改驅動程式使用的連接池超時。  
  
 ODBC_INSTALL_DRIVER:安裝新驅動程式。  
  
 ODBC_REMOVE_DRIVER:刪除現有驅動程式。  
  
 此選項也可以特定於驅動程式,在這種情況下,第一個選項的*fRequest*必須從 ODBC_CONFIG_DRIVER_MAX+1 開始。 任何附加選項的*fRequest*也必須從大於 ODBC_CONFIG_DRIVER_MAX+1 的值開始。  
  
 *lpszDriver*  
 [輸入]在系統資訊中註冊的驅動程式的名稱。  
  
 *lpszArgs*  
 [輸入]包含特定於驅動程式*的 fRequest*的參數的 null 連接端接字串。  
  
 *lpszMsg*  
 【輸出]包含驅動程式設定輸出訊息的 null 終止字串。  
  
 *cbMsgMax*  
 [輸入]*lpszMsg*的長度。  
  
 *巴布姆斯格*  
 【輸出]可用以*lpszMsg*返回的位元組總數。 如果可用於返回的位元組數大於或等於*cbMsgMax,**則 lpszMsg*中的輸出消息將被截斷為*cbMsgMax*減去 null 終止字元。 *pcbMsgOut*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDriver**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式*碼值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszMsg*參數無效。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_INSTALL_DRIVERODBC_REMOVE_DRIVER<br /><br /> *fRequest*參數是一個驅動程式特定的選項,小於或等於ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。 在註冊表中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效關鍵字-值對|*lpszArgs*參數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行*fRequest*參數請求的操作。 對**ConfigDriver 的**呼叫失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉換器設定庫|無法載入驅動程式設置庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDriver**允許應用程式呼叫驅動程式的**ConfigDriver**例程式,而無需知道名稱並載入特定於驅動程式的安裝程式 DLL。 安裝驅動程式設置 DLL 後,安裝程式呼叫此功能。 呼叫程式應注意,此函數可能並非對所有驅動程式都可用。 在這種情況下,調用程式應繼續,沒有錯誤。  
  
## <a name="driver-specific-options"></a>特定於驅動程式的選項  
 應用程式可以使用*fRequest*參數請求驅動程式公開的特定於驅動程式的功能。 第一個選項的*fRequest*將在ODBC_CONFIG_DRIVER_MAX+1,其他選項將從該值增加 1。 驅動程式為該函數所需的任何參數都應在*lpszArgs*參數中傳遞的 null 端接字串中提供。 提供此類功能的驅動程式應維護特定於驅動程式的選項表。 選項應完整地記錄在驅動程序文件中。 使用特定於驅動程式的選項的應用程式編寫器應注意,此使用將使應用程式的互操作性降低。  
  
## <a name="setting-connection-pooling-timeout"></a>設定連接池逾時  
 設置驅動程式的配置時,可以設置連接池超時屬性。 **SQLConfigDriver**調用時,ODBC_CONFIG_DRIVER和*lpszArgs*的*frequest*設置為**CPTimeout。** **CPTimeout**確定連接可以在連接池中保留而不使用的時間週期。 超時過期時,連接將關閉並從池中刪除。 默認超時為 60 秒。  
  
 當**SQLConfigDriver**呼叫*fRequest*設定為ODBC_INSTALL_DRIVER或ODBC_REMOVE_DRIVER時,驅動程式管理員將載入相應的驅動程式設定 DLL 並調用**ConfigDriver**函數。 當使用*fODBC_CONFIG_DRIVER調用* **SQLConfigDriver**時,所有處理都將在 ODBC 安裝程式中執行,因此不必載入驅動程式設定 DLL。  
  
## <a name="messages"></a>訊息  
 驅動程式設定例程可以將文本訊息作為*lpszMsg*緩衝區中的 null 終止字串發送到應用程式。 如果消息大於或等於*cbMsgMax*字元,則**ConfigDriver**函數將消息截斷為*cbMsgMax*減去 null 終止字元。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[設定驅動程式](../../../odbc/reference/syntax/configdriver-function.md)(在設定 DLL 中)|  
|移除預設資料來源|[SQL 移除預設資料來源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
