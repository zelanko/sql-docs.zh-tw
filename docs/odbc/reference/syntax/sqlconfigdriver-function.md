---
description: SQLConfigDriver 函式
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
ms.openlocfilehash: 04ee54bba13730504ed08cfc1307858edea56282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476154"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函式
**一致性**  
 引進的版本： ODBC 2。5  
  
 **總結**  
 **SQLConfigDriver** 會載入適當的驅動程式安裝 DLL，並呼叫 **ConfigDriver** 函數。  
  
 您也可以使用[ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)來存取**SQLConfigDriver**的功能。  
  
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
 輸出父視窗控制碼。 如果控制碼為 null，函數將不會顯示任何對話方塊。  
  
 *fRequest*  
 輸出要求的類型。 *fRequest* 必須包含下列其中一個值：  
  
 ODBC_CONFIG_DRIVER：變更驅動程式所使用的連接共用超時。  
  
 ODBC_INSTALL_DRIVER：安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER：移除現有的驅動程式。  
  
 此選項也可以是驅動程式特定的，在此情況下，第一個選項的 *fRequest* 必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 任何其他選項的 *fRequest* 也必須從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值開始。  
  
 *lpszDriver*  
 輸出系統資訊中所註冊的驅動程式名稱。  
  
 *lpszArgs*  
 輸出以 null 終止的字串，其中包含驅動程式特定 *fRequest*的引數。  
  
 *lpszMsg*  
 出以 null 終止的字串，其中包含驅動程式安裝程式的輸出訊息。  
  
 *cbMsgMax*  
 輸出LpszMsg 的長度 *。*  
  
 *pcbMsgOut*  
 出可在 *lpszMsg*中傳回的總位元組數。 如果可傳回的位元組數目大於或等於 *cbMsgMax*， *lpszMsg* 中的輸出訊息會被截斷為 *cbMsgMax* 減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDriver**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|緩衝區長度無效|*LpszMsg*引數無效。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *FRequest*引數是小於或等於 ODBC_CONFIG_DRIVER_MAX 的驅動程式特定選項。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|不正確關鍵字-值配對|*LpszArgs*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求* 失敗|安裝程式無法執行 *fRequest* 引數所要求的作業。 對 **ConfigDriver** 的呼叫失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或翻譯工具安裝程式庫|無法載入驅動程式安裝程式程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDriver** 可讓應用程式呼叫驅動程式的 **ConfigDriver** 常式，而不需要知道名稱和載入驅動程式特定的安裝 DLL。 安裝程式在安裝驅動程式安裝程式 DLL 之後，會呼叫這個函式。 呼叫程式應該要注意的是，此函式可能無法用於所有驅動程式。 在這種情況下，呼叫程式應該會繼續進行，而不會發生錯誤。  
  
## <a name="driver-specific-options"></a>驅動程式專用選項  
 應用程式可以使用 *fRequest* 引數來要求驅動程式所公開的驅動程式特定功能。 第一個選項的 *fRequest* 會 ODBC_CONFIG_DRIVER_MAX + 1，而其他選項將會從該值遞增1。 該函式的驅動程式所需的任何引數，都應該在 *lpszArgs* 引數中傳遞的 null 終止字串中提供。 提供這類功能的驅動程式應維持驅動程式專用選項的表格。 這些選項應完整記載于驅動程式檔中。 使用驅動程式專屬選項的應用程式寫入器應該知道，這種使用方式會讓應用程式更不具互通性。  
  
## <a name="setting-connection-pooling-timeout"></a>設定連接共用超時  
 當您設定驅動程式的設定時，可以設定連接共用超時屬性。 呼叫**SQLConfigDriver**時，會將 ODBC_CONFIG_DRIVER 的*fRequest*和*lpszArgs*設定為**CPTimeout**。 **CPTimeout** 會決定連接可以保留在連接集區中的時間，而不使用。 當超時時間過期時，連接會關閉並從集區中移除。 預設的超時時間為60秒。  
  
 當呼叫 **SQLConfigDriver** 時， *fRequest* 設定為 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER 時，驅動程式管理員會載入適當的驅動程式安裝程式 DLL，並呼叫 **ConfigDriver** 函式。 使用 ODBC_CONFIG_DRIVER 的*fRequest*呼叫**SQLConfigDriver**時，會在 ODBC 安裝程式中執行所有處理，如此就不需要載入驅動程式安裝 DLL。  
  
## <a name="messages"></a>訊息  
 驅動程式安裝程式常式可將文字訊息傳送至應用程式，做為 *lpszMsg* 緩衝區中以 null 終止的字串。 如果**ConfigDriver**函式大於或等於*cbMsgMax*字元，則會將訊息截斷為*cbMsgMax*減去 null 終止字元。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除驅動程式|安裝 DLL 中的[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) () |  
|移除預設資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
