---
title: "ConfigDriver 函式 |Microsoft 文件"
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
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 037d4ffcbe7d81c6e4a9c1a524f5f4977621f277
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="configdriver-function"></a>ConfigDriver 函式
**一致性**  
 版本引進了： ODBC 2.5  
  
 **摘要**  
 **ConfigDriver**允許安裝程式以執行安裝和解除安裝函式，而不需要呼叫程式**ConfigDSN**。 此函式會執行驅動程式專屬功能，例如建立驅動程式特定的系統資訊和在安裝期間，執行 DSN 轉換，以及在解除安裝期間清除已完成修改系統資訊。 此函式公開驅動程式安裝 DLL 或個別的安裝程式 DLL。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
  
 *常見*  
 [輸入]要求的類型。 *常見*引數必須包含下列值之一：  
  
 ODBC_INSTALL_DRIVER： 安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER： 移除驅動程式。  
  
 此選項也可以是特定驅動程式在此情況下*常見*第一個選項的引數必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 *常見*從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值也必須啟動任何其他選項的引數。  
  
 *lpszDriver*  
 [輸入]在系統資訊的 Odbcinst.ini 索引鍵中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 [輸入]Null 結束的字串，包含特定驅動程式的引數*常見*。  
  
 *lpszMsg*  
 [輸出]以 null 結束的字串，包含輸出訊息從驅動程式安裝程式。  
  
 *cbMsgMax*  
 [輸入]長度*lpszMsg*。  
  
 *pcbMsgOut*  
 [輸出]可用來傳回中的位元組總數*lpszMsg*。  
  
 如果傳回可用的位元組數目大於或等於*cbMsgMax*中的輸出訊息*lpszMsg*會被截斷成*cbMsgMax*減去 null 結束字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDriver**傳回 FALSE，相關聯 *\*pfErrorCode*值由呼叫張貼至安裝程式錯誤緩衝區**SQLPostInstallerError**可取得藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> 驅動程式特有的選項是小於或等於 ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。 它不在登錄中。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行所要求的操作*常見*引數。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定驅動程式或轉譯器錯誤|驅動程式特有的錯誤，它沒有任何已定義的 ODBC 安裝程式發生錯誤。 *SzError*呼叫中的引數**SQLPostInstallerError**函式應該包含驅動程式特有的錯誤訊息。|  
  
## <a name="comments"></a>註解  
  
### <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以要求使用的驅動程式所公開的驅動程式專屬功能*常見*引數。 *常見*ODBC_CONFIG_DRIVER_MAX 加 1，，將會是第一個選項，而其他選項會從值 1 遞增。 任何所需的驅動程式應以 null 結束的字串中提供該函式的引數中傳遞*lpszArgs*引數。 提供這類功能的驅動程式應該維護的驅動程式特有的選項。 選項應該是完整記錄在驅動程式文件。 應用程式寫入器會使用驅動程式特有的選項都應該注意，這會讓應用程式較不互通。  
  
### <a name="messages"></a>訊息  
 驅動程式安裝常式可以將文字訊息傳送至應用程式中的 null 終止字串*lpszMsg*緩衝區。 訊息會被截斷為*cbMsgMax*減的 null 終止字元**ConfigDriver**函式是否大於或等於*cbMsgMax*字元。

