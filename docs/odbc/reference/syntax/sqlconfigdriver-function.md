---
title: SQLConfigDriver 函式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301243"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函式
**標準**  
 引進的版本： ODBC 2。5  
  
 **摘要**  
 **SQLConfigDriver**會載入適當的驅動程式安裝 DLL，並呼叫**ConfigDriver**函式。  
  
 您也可以使用 ODBCCONF 來存取**SQLConfigDriver**的功能[。EXE](../../../odbc/odbcconf-exe.md)。  
  
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
 *hwndParent*  
 源父視窗控制碼。 如果控制碼為 null，函數不會顯示任何對話方塊。  
  
 *fRequest*  
 源要求的類型。 *fRequest*必須包含下列其中一個值：  
  
 ODBC_CONFIG_DRIVER：變更驅動程式所使用的連接共用超時。  
  
 ODBC_INSTALL_DRIVER：安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER：移除現有的驅動程式。  
  
 此選項也可以是特定驅動程式，在此情況下，第一個選項的*fRequest*必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 任何其他選項的*fRequest*也必須從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值開始。  
  
 *lpszDriver*  
 源在系統資訊中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 源以 null 終止的字串，其中包含驅動程式特定*fRequest*的引數。  
  
 *lpszMsg*  
 輸出以 null 終止的字串，其中包含驅動程式安裝程式的輸出訊息。  
  
 *cbMsgMax*  
 源LpszMsg 的長度 *。*  
  
 *pcbMsgOut*  
 輸出可用來在*lpszMsg*中傳回的位元組總數。 如果傳回的位元組數目大於或等於*cbMsgMax*， *lpszMsg*中的輸出訊息會截斷為*cbMsgMax*減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDriver**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不正確緩衝區長度|*LpszMsg*引數無效。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *FRequest*引數是小於或等於 ODBC_CONFIG_DRIVER_MAX 的驅動程式特定選項。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszArgs*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行*fRequest*引數所要求的作業。 呼叫**ConfigDriver**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或 translator 安裝程式程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>評價  
 **SQLConfigDriver**可讓應用程式呼叫驅動程式的**ConfigDriver**常式，而不需要知道名稱和載入驅動程式特定的安裝程式 DLL。 安裝程式會在安裝驅動程式安裝 DLL 之後呼叫此功能。 呼叫程式應該知道此函式可能不適用於所有驅動程式。 在這種情況下，呼叫程式應該會繼續執行，而不會發生錯誤。  
  
## <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以使用*fRequest*引數來要求驅動程式所公開的驅動程式特有功能。 第一個選項的*fRequest*將會 ODBC_CONFIG_DRIVER_MAX + 1，而其他選項會從該值遞增1。 該函式的驅動程式所需的任何引數，都應該在*lpszArgs*引數中傳遞的以 null 終止的字串中提供。 提供這類功能的驅動程式應該維護驅動程式特有選項的表格。 這些選項應完整記載于驅動程式檔集。 使用驅動程式專屬選項的應用程式寫入器應該注意，這種用法會讓應用程式的互通更低。  
  
## <a name="setting-connection-pooling-timeout"></a>設定連接共用超時  
 當您設定驅動程式的設定時，可以設定連接共用超時屬性。 呼叫**SQLConfigDriver**時， *fRequest*為 ODBC_CONFIG_DRIVER 並將*lpszArgs*設定為**CPTimeout**。 **CPTimeout**會判斷連接可以保留在連接集區中的時間長度，而不會使用。 當超時時間過期時，連接就會關閉，並從集區中移除。 預設的超時時間為60秒。  
  
 當使用設定為 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER 的*fRequest*來呼叫**SQLConfigDriver**時，驅動程式管理員會載入適當的驅動程式安裝 DLL，並呼叫**ConfigDriver**函式。 以 ODBC_CONFIG_DRIVER 的*fRequest*呼叫**SQLConfigDriver**時，所有處理都是在 ODBC 安裝程式中執行，因此不需要載入驅動程式安裝程式 DLL。  
  
## <a name="messages"></a>訊息  
 驅動程式安裝常式可以將文字訊息傳送至應用程式，做為*lpszMsg*緩衝區中以 null 結束的字串。 如果**ConfigDriver**函數大於或等於*cbMsgMax*字元，則會將訊息截斷為*cbMsgMax*減去 null 終止字元。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)（在安裝程式 DLL 中）|  
|移除預設資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
