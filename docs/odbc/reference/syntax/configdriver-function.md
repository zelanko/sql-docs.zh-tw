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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce34e46a49e88167606543a341aaef55591493ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538083"
---
# <a name="configdriver-function"></a>ConfigDriver 函式
**合規性**  
 導入的版本：ODBC 2.5  
  
 **摘要**  
 **ConfigDriver**可讓安裝程式來執行安裝和解除安裝而不需要程式呼叫的函式**ConfigDSN**。 此函式會執行驅動程式特有的功能，例如建立驅動程式特定的系統資訊和在安裝期間，執行資料來源名稱的轉換，以及在解除安裝期間，清除 系統資訊修改。 此函式公開驅動程式安裝 DLL 或個別的安裝程式 DLL。  
  
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
 [輸入]父視窗控制代碼。 如果控制代碼為 null，函式不會顯示任何對話方塊。  
  
 *fRequest*  
 [輸入]要求的類型。 *常見*引數必須包含下列值之一：  
  
 ODBC_INSTALL_DRIVER:安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER:移除驅動程式。  
  
 此選項也可以是特定驅動程式，在此情況下*常見*第一個選項的引數必須開始從 ODBC_CONFIG_DRIVER_MAX + 1。 *常見*從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值也必須啟動任何其他選項的引數。  
  
 *lpszDriver*  
 [輸入]在 系統資訊的 Odbcinst.ini 索引鍵中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 [輸入]以 null 結尾的字串，包含特定驅動程式的引數*常見*。  
  
 *lpszMsg*  
 [輸出]以 null 結束的字串，包含輸出訊息從驅動程式安裝程式。  
  
 *cbMsgMax*  
 [輸入]長度*lpszMsg*。  
  
 *pcbMsgOut*  
 [輸出]傳回在可用的位元組總數*lpszMsg*。  
  
 如果傳回可用的位元組數目大於或等於*cbMsgMax*中的輸出訊息*lpszMsg*會被截斷成*cbMsgMax*減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDriver**會傳回 FALSE，相關聯 *\*pfErrorCode*值時，會張貼至安裝程式錯誤的緩衝區上，藉由呼叫**SQLPostInstallerError**並可透過呼叫中取得**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 驅動程式特有的選項會是小於或等於 ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszDriver*引數無效。 它找不到在登錄中。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行要求的作業*常見*引數。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或轉譯器特定的錯誤|驅動程式特有的錯誤，它沒有任何已定義的 ODBC 安裝程式錯誤。 *SzError*呼叫中的引數**SQLPostInstallerError**函式應該包含驅動程式特有的錯誤訊息。|  
  
## <a name="comments"></a>註解  
  
### <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以要求使用驅動程式所公開的驅動程式專屬功能*常見*引數。 *常見*會 ODBC_CONFIG_DRIVER_MAX 加 1，第一次的選項和其他選項就會遞增 1 的值。 該函式應該提供以 null 結束的字串中，驅動程式所需的任何引數傳入*lpszArgs*引數。 提供這類功能的驅動程式應該維護資料表的驅動程式特有的選項。 在 驅動程式文件都應該詳細記錄選項。 應用程式寫入器會使用驅動程式特有的選項，應該注意，這會讓應用程式較不具互通性。  
  
### <a name="messages"></a>訊息  
 驅動程式安裝程式常式可以將文字訊息傳送至以 null 終止的字串中的應用程式*lpszMsg*緩衝區。 訊息會被截斷成*cbMsgMax*減號的 null 終止字元**ConfigDriver**函式是否大於或等於*cbMsgMax*字元。
