---
title: ConfigDriver 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303959"
---
# <a name="configdriver-function"></a>ConfigDriver 函式
**標準**  
 引進的版本： ODBC 2。5  
  
 **摘要**  
 **ConfigDriver**可讓安裝程式執行安裝和卸載功能，而不需要程式呼叫**ConfigDSN**。 此函式會執行驅動程式特有的功能，例如建立驅動程式特定的系統資訊，並在安裝期間執行 DSN 轉換，以及在卸載期間清除系統資訊修改。 此函式是由驅動程式安裝 DLL 或個別安裝程式 DLL 所公開。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 源父視窗控制碼。 如果控制碼為 null，函數不會顯示任何對話方塊。  
  
 *fRequest*  
 源要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_INSTALL_DRIVER：安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER：移除驅動程式。  
  
 此選項也可以是驅動程式特有的，在此情況下，第一個選項的*fRequest*引數必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 任何其他選項的*fRequest*引數，也必須以大於 ODBC_CONFIG_DRIVER_MAX + 1 的值來啟動。  
  
 *lpszDriver*  
 源在系統資訊的 Odbcinst 機碼中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 源以 null 終止的字串，其中包含驅動程式特定*fRequest*的引數。  
  
 *lpszMsg*  
 輸出以 null 終止的字串，其中包含驅動程式設定的輸出訊息。  
  
 *cbMsgMax*  
 源*LpszMsg*的長度。  
  
 *pcbMsgOut*  
 輸出可用來在*lpszMsg*中傳回的位元組總數。  
  
 如果傳回的位元組數目大於或等於*cbMsgMax*， *lpszMsg*中的輸出訊息會截斷為*cbMsgMax*減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDriver**傳回 FALSE 時，會呼叫**SQLPostInstallerError**來將相關聯* \*的 pfErrorCode*值張貼到安裝程式錯誤緩衝區，並可透過呼叫**SQLInstallerError**來取得。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 驅動程式特定的選項小於或等於 ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或 translator 名稱無效|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行*fRequest*引數所要求的作業。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或 translator 特定的錯誤|驅動程式特定的錯誤，其中沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPostInstallerError**函式中的*SzError*引數應該包含驅動程式特定的錯誤訊息。|  
  
## <a name="comments"></a>評價  
  
### <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以使用*fRequest*引數來要求驅動程式所公開的驅動程式特有功能。 第一個選項的*fRequest*將會 ODBC_CONFIG_DRIVER_MAX 加1，而其他選項會從該值遞增1。 該函式的驅動程式所需的任何引數，都應該在*lpszArgs*引數中傳遞的以 null 終止的字串中提供。 提供這類功能的驅動程式應該維護驅動程式特有選項的表格。 這些選項應完整記載于驅動程式檔集。 使用驅動程式專屬選項的應用程式寫入器應該注意，這會使應用程式的互通更低。  
  
### <a name="messages"></a>訊息  
 驅動程式安裝常式可以將文字訊息傳送至應用程式，做為*lpszMsg*緩衝區中以 null 結束的字串。 如果**ConfigDriver**函數大於或等於*cbMsgMax*字元，則會將訊息截斷為*cbMsgMax*減去 null 終止字元。
