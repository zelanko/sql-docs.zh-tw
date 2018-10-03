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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90c1c31e6b4b33d662636d34fcebbd17393f69a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608246"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 函式
**合規性**  
 版本導入： ODBC 2.5  
  
 **摘要**  
 **SQLConfigDriver**載入適當的驅動程式安裝程式 DLL 並呼叫**ConfigDriver**函式。  
  
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
  
 此選項也可以是特定驅動程式，在此情況下*常見*的第一個選項必須開始從 ODBC_CONFIG_DRIVER_MAX + 1。 *常見*的任何其他選項也必須啟動從大於 ODBC_CONFIG_DRIVER_MAX + 1 的值。  
  
 *lpszDriver*  
 [輸入]在 系統資訊中註冊的驅動程式名稱。  
  
 *lpszArgs*  
 [輸入]Null 結束的字串，包含特定驅動程式的引數*常見*。  
  
 *lpszMsg*  
 [輸出]以 null 結尾的字串，其中包含從驅動程式安裝程式的輸出訊息。  
  
 *cbMsgMax*  
 [輸入]長度*lpszMsg。*  
  
 *pcbMsgOut*  
 [輸出]傳回在可用的位元組總數*lpszMsg*。 如果傳回可用的位元組數目大於或等於*cbMsgMax*中的輸出訊息*lpszMsg*會被截斷成*cbMsgMax*減去 null 終止字元。 *PcbMsgOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLConfigDriver**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszMsg*引數無效。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數無效。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|無效的要求類型|*常見*引數不是下列其中之一：<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *常見*引數是小於或等於 ODBC_CONFIG_DRIVER_MAX 驅動程式專用選項。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszDriver*引數無效。 它找不到在登錄中。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無效的關鍵字-值配對|*LpszArgs*引數包含語法錯誤。|  
|ODBC_ERROR_REQUEST_FAILED|*要求*失敗|安裝程式無法執行要求的作業*常見*引數。 若要在呼叫**ConfigDriver**失敗。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯器的安裝程式庫|無法載入驅動程式安裝程式庫。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 **SQLConfigDriver**可讓應用程式呼叫駕**ConfigDriver**例行而不必知道名稱，並載入特定驅動程式安裝程式 DLL。 安裝程式 DLL 已安裝的驅動程式安裝之後呼叫此函式。 呼叫端的程式應該要知道此函式可能無法使用的所有驅動程式。 在此情況下，應該繼續呼叫程式，不會發生錯誤。  
  
## <a name="driver-specific-options"></a>驅動程式特有的選項  
 應用程式可以要求使用驅動程式所公開的驅動程式專屬功能*常見*引數。 *常見*的第一個選項為 ODBC_CONFIG_DRIVER_MAX + 1，以及其他選項就會遞增 1 的值。 該函式應該提供以 null 結束的字串中，驅動程式所需的任何引數傳入*lpszArgs*引數。 提供這類功能的驅動程式應該維護資料表的驅動程式特有的選項。 在 驅動程式文件都應該詳細記錄選項。 應用程式寫入器會使用驅動程式特有的選項，應該注意，此使用會讓應用程式較不具互通性。  
  
## <a name="setting-connection-pooling-timeout"></a>設定連線共用逾時  
 當您將驅動程式的組態設定時，可以設定連線共用逾時屬性。 **SQLConfigDriver**以呼叫*常見*ODBC_CONFIG_DRIVER 的並*lpszArgs*設為**CPTimeout**。 **CPTimeout**決定的連接可連接集區中保留未使用的時間期間。 當逾時到期時，連線已關閉，且從集區移除。 預設的逾時為 60 秒。  
  
 當**SQLConfigDriver**呼叫*常見*設定為 ODBC_INSTALL_DRIVER 或 ODBC_REMOVE_DRIVER，驅動程式管理員會載入適當的驅動程式安裝程式 DLL 呼叫**ConfigDriver**函式。 當**SQLConfigDriver**呼叫*常見*ODBC_CONFIG_DRIVER 的所有處理都執行 ODBC 安裝程式中，因此不需要載入驅動程式安裝程式 DLL。  
  
## <a name="messages"></a>訊息  
 驅動程式安裝程式常式可為 null 結尾字串的應用程式傳送簡訊*lpszMsg*緩衝區。 訊息會被截斷成*cbMsgMax*減號的 null 終止字元**ConfigDriver**函式是否大於或等於*cbMsgMax*字元。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|新增、 修改或移除驅動程式|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)（在安裝程式 DLL 中）|  
|移除預設的資料來源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
