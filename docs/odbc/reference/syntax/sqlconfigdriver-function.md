---
title: SQLConfigDriver 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3af2f70156cae3427b5d22f3214f5c911af14a5d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函式
**一致性**  
 版本引進了： ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**載入適當的驅動程式安裝 DLL 和呼叫**ConfigDriver**函式。  
  
 功能**SQLConfigDriver**也可以使用存取[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]父視窗控制代碼。 如果控制代碼為 null，函式不會顯示任何對話方塊。  
  
 *常見*  
 [輸入]要求的類型。 *常見*必須包含下列值之一：  
  
 ODBC_CONFIG_DRIVER： 變更連接共用的驅動程式所使用的逾時。  
  
 ODBC_INSTALL_DRIVER： 安裝新的驅動程式。  
  
 ODBC_REMOVE_DRIVER： 移除現有的驅動程式。  
  
 此選項也可以是特定驅動程式在此情況下*常見*的第一個選項必須從 ODBC_CONFIG_DRIVER_MAX + 1 開始。 *常見*的任何其他選項也必須啟動從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值。  
  
 *lpszDriver*  
 [輸入]在 系統資訊中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 [輸入]包含特定驅動程式的引數的 null 終止字串*常見*。  
  
 *lpszMsg*  
 [輸出]以 null 結束的字串，其中包含輸出訊息從驅動程式安裝程式。  
  
 *cbMsgMax*  
 [輸入]長度*lpszMsg。*  
  
 *pcbMsgOut*  
 [輸出]可用來傳回中的位元組總數*lpszMsg*。 如果傳回可用的位元組數目大於或等於*cbMsgMax*中的輸出訊息*lpszMsg*會被截斷成*cbMsgMax*減去 null 結束字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDriver**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszMsg*引數無效。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求的類型無效|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *常見*引數以前是小於或等於 ODBC_CONFIG_DRIVER_MAX 驅動程式特定選項。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszDriver*引數無效。 它不在登錄中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszArgs*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行所要求的操作*常見*引數。 若要呼叫**ConfigDriver**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯程式的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDriver**允許應用程式呼叫的驅動程式**ConfigDriver**常式，而不必知道名稱，而且載入特定驅動程式安裝 DLL。 安裝程式會呼叫此函式之後的 DLL 已安裝的驅動程式安裝。 呼叫端程式應該要知道這個函式可能無法使用的所有驅動程式。 在這種情況下，呼叫端程式應該繼續不會發生錯誤。  
  
## <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以要求使用的驅動程式所公開的驅動程式專屬功能*常見*引數。 *常見*為 ODBC_CONFIG_DRIVER_MAX + 1，第一個選項，以及其他選項會從值 1 遞增。 任何所需的驅動程式應以 null 結束的字串中提供該函式的引數中傳遞*lpszArgs*引數。 提供這類功能的驅動程式應該維護的驅動程式特有的選項。 選項應該是完整記錄在驅動程式文件。 應用程式寫入器會使用驅動程式特有的選項都應該注意，此使用會讓應用程式較不互通。  
  
## <a name="setting-connection-pooling-timeout"></a>設定連線共用逾時  
 當您將驅動程式的組態設定時，可以設定連線共用逾時屬性。 **SQLConfigDriver**呼叫*常見*的 ODBC_CONFIG_DRIVER 和*lpszArgs*設**CPTimeout**。 **CPTimeout**決定連接可以維持連接集區中，而不使用的時間期間。 在逾時過期時，連線已關閉，且從集區移除。 預設逾時為 60 秒。  
  
 當**SQLConfigDriver**呼叫*常見*設為 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER，驅動程式管理員會載入適當的驅動程式安裝 DLL 呼叫**ConfigDriver**函式。 當**SQLConfigDriver**呼叫*常見*ODBC_CONFIG_DRIVER，所有處理都都執行的 ODBC 安裝程式中，讓驅動程式安裝 DLL 並沒有要載入。  
  
## <a name="messages"></a>訊息  
 驅動程式安裝常式可以傳送給應用程式以 null 終止之字串中的文字訊息*lpszMsg*緩衝區。 訊息會被截斷為*cbMsgMax*減的 null 終止字元**ConfigDriver**函式是否大於或等於*cbMsgMax*字元。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)（在安裝程式 DLL 中）|  
|移除預設的資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
