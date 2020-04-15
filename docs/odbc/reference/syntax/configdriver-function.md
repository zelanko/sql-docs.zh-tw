---
title: 設定驅動程式功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303959"
---
# <a name="configdriver-function"></a>ConfigDriver 函式
**一致性**  
 版本介紹: ODBC 2.5  
  
 **摘要**  
 **設定驅動程式**允許安裝程式執行安裝和卸載功能,而無需程式呼叫**ConfigDSN**。 此功能將執行特定於驅動程式的功能,例如創建特定於驅動程式的系統資訊並在安裝期間執行 DSN 轉換,以及在卸載期間清理系統資訊修改。 此功能由驅動程式設置 DLL 或單獨的設置 DLL 公開。  
  
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
 *hwnd 家長*  
 [輸入]父視窗句柄。 如果句柄為空,則函數將不會顯示任何對話方塊。  
  
 *f 要求*  
 [輸入]請求的類型。 *fRequest*參數必須包含以下值之一:  
  
 ODBC_INSTALL_DRIVER:安裝新驅動程式。  
  
 ODBC_REMOVE_DRIVER:刪除驅動程式。  
  
 此選項也可以特定於驅動程式,在這種情況下,第一個選項的*fRequest*參數必須從 ODBC_CONFIG_DRIVER_MAX+1 開始。 任何附加選項的*fRequest*參數也必須從大於ODBC_CONFIG_DRIVER_MAX+1的值開始。  
  
 *lpszDriver*  
 [輸入]在系統資訊的 Odbcinst.ini 密鑰中註冊的驅動程式的名稱。  
  
 *lpszArgs*  
 [輸入]包含特定於驅動程式*的 fRequest*參數的 null 連接端接字串。  
  
 *lpszMsg*  
 【輸出]包含驅動程式設定輸出訊息的 null 連接端字串。  
  
 *cbMsgMax*  
 [輸入]*lpszMsg*的長度 。  
  
 *巴布姆斯格*  
 【輸出]可用以*lpszMsg*返回的位元組總數。  
  
 如果可用於返回的位元組數大於或等於*cbMsgMax,**則 lpszMsg*中的輸出消息將被截斷為*cbMsgMax*減去 null 終止字元。 *pcbMsgOut*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigDriver**傳回 FALSE 時,透過呼叫**SQLPost 安裝程式錯誤**將關聯的*\*pfError 程式*碼值發布到安裝程式錯誤緩衝區,並且可以透過呼叫**SQL 安裝程式錯誤**獲得。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|不合法的要求型態|*fRequest*參數不是以下參數之一:<br /><br /> ODBC_INSTALL_DRIVERODBC_REMOVE_DRIVER<br /><br /> 特定於驅動程式的選項小於或等於ODBC_CONFIG_DRIVER_MAX。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。 在註冊表中找不到它。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|無法執行*fRequest*參數請求的操作。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或轉換器特定錯誤|驅動程式特定的錯誤,沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPost 安裝程式錯誤**函數時 *,SzError*參數應包含特定於驅動程式的錯誤訊息。|  
  
## <a name="comments"></a>註解  
  
### <a name="driver-specific-options"></a>特定於驅動程式的選項  
 應用程式可以使用*fRequest*參數請求驅動程式公開的特定於驅動程式的功能。 第一個選項的*fRequest*將ODBC_CONFIG_DRIVER_MAX加 1,其他選項將從該值增加 1。 驅動程式為該函數所需的任何參數都應在*lpszArgs*參數中傳遞的 null 端接字串中提供。 提供此類功能的驅動程式應維護特定於驅動程式的選項表。 選項應完整地記錄在驅動程序文件中。 使用特定於驅動程式的選項的應用程式編寫器應注意,這將使應用程式的互操作性降低。  
  
### <a name="messages"></a>訊息  
 驅動程式設定例程可以將文本訊息作為*lpszMsg*緩衝區中的 null 終止字串發送到應用程式。 如果消息大於或等於*cbMsgMax*字元,則**ConfigDriver**函數將消息截斷為*cbMsgMax*減去 null 終止字元。
