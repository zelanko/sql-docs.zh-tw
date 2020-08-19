---
description: ConfigDriver 函式
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
ms.openlocfilehash: 3d59765d1b6a6a662c02b459e07bac10895838a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428950"
---
# <a name="configdriver-function"></a>ConfigDriver 函式
**一致性**  
 引進的版本： ODBC 2。5  
  
 **總結**  
 **ConfigDriver** 可讓安裝程式執行安裝和卸載功能，而不需要程式呼叫 **ConfigDSN**。 此函式會執行驅動程式特有的功能，例如建立驅動程式特定的系統資訊，並在安裝期間執行 DSN 轉換，以及在卸載期間清除系統資訊修改。 此函式是由驅動程式安裝程式 DLL 或個別的安裝 DLL 所公開。  
  
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
 輸出父視窗控制碼。 如果控制碼為 null，函數將不會顯示任何對話方塊。  
  
 *fRequest*  
 輸出要求的類型。 *FRequest*引數必須包含下列其中一個值：  
  
 ODBC_INSTALL_DRIVER：安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER：移除驅動程式。  
  
 這個選項也可以是驅動程式特定的，在此情況下，第一個選項的 *fRequest* 引數必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 任何其他選項的 *fRequest* 引數，也必須從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值開始。  
  
 *lpszDriver*  
 輸出在系統資訊的 Odbcinst.ini 金鑰中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 輸出以 null 終止的字串，其中包含驅動程式特定 *fRequest*的引數。  
  
 *lpszMsg*  
 出以 null 終止的字串，其中包含驅動程式安裝程式的輸出訊息。  
  
 *cbMsgMax*  
 輸出 *LpszMsg*的長度。  
  
 *pcbMsgOut*  
 出可在 *lpszMsg*中傳回的總位元組數。  
  
 如果可傳回的位元組數目大於或等於 *cbMsgMax*， *lpszMsg* 中的輸出訊息會被截斷為 *cbMsgMax* 減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，否則會傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDriver**傳回 FALSE 時，會呼叫**SQLPostInstallerError**將相關聯的* \* pfErrorCode*值張貼至安裝程式錯誤緩衝區，而且可以藉由呼叫**SQLInstallerError**來取得。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*FRequest*引數不是下列其中一項：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 驅動程式專用選項小於或等於 ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszDriver*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_REQUEST_FAILED|*要求* 失敗|無法執行 *fRequest* 引數所要求的作業。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或轉譯程式特定的錯誤|未定義 ODBC 安裝程式錯誤的驅動程式特有錯誤。 呼叫**SQLPostInstallerError**函式的*SzError*引數應該包含驅動程式特定的錯誤訊息。|  
  
## <a name="comments"></a>註解  
  
### <a name="driver-specific-options"></a>驅動程式專用選項  
 應用程式可以使用 *fRequest* 引數來要求驅動程式所公開的驅動程式特定功能。 第一個選項的 *fRequest* 會 ODBC_CONFIG_DRIVER_MAX 加1，而其他選項將會從該值遞增1。 該函式的驅動程式所需的任何引數，都應該在 *lpszArgs* 引數中傳遞的 null 終止字串中提供。 提供這類功能的驅動程式應維持驅動程式專用選項的表格。 這些選項應完整記載于驅動程式檔中。 使用驅動程式專屬選項的應用程式寫入器應該要注意，這樣可讓應用程式更不互通。  
  
### <a name="messages"></a>訊息  
 驅動程式安裝程式常式可將文字訊息傳送至應用程式，做為 *lpszMsg* 緩衝區中以 null 終止的字串。 如果**ConfigDriver**函式大於或等於*cbMsgMax*字元，則會將訊息截斷為*cbMsgMax*減去 null 終止字元。
