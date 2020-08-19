---
description: SQLGetTranslator 函式
title: SQLGetTranslator 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d30268c846af4e95298d00edcd13def97c20c77d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421222"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函式
**一致性**  
 引進的版本： ODBC 2。0  
  
 **總結**  
 **SQLGetTranslator** 會顯示對話方塊，讓使用者可以從中選取翻譯工具。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 輸出父視窗控制碼。  
  
 *lpszName*  
 [輸入/輸出]系統資訊中的翻譯工具名稱。  
  
 *cbNameMax*  
 輸出 *LpszName* 緩衝區的最大長度。  
  
 *pcbNameOut*  
 [輸入/輸出] (不包括 null 終止位元組的位元組總數) 在 *lpszName*中傳遞或傳回。 如果可傳回的位元組數目大於或等於 *cbNameMax*， *lpszName* 中的翻譯工具名稱會截斷為 *cbNameMax* 減去 null 終止字元。 *PcbNameOut*引數可以是 null 指標。  
  
 *lpszPath*  
 出轉譯 DLL 的完整路徑。  
  
 *cbPathMax*  
 輸出 *LpszPath* 緩衝區的最大長度。  
  
 *pcbPathOut*  
 出 (不包括 null 終止位元組的位元組總數) 在 *lpszPath*中傳回。 如果可傳回的位元組數目大於或等於 *cbPathMax*， *lpszPath* 中的轉譯 DLL 路徑會被截斷為 *cbPathMax* 減去 null 終止字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *pvOption*  
 [輸出] 32 位轉譯選項。  
  
## <a name="returns"></a>傳回  
 如果成功，函數會傳回 TRUE，如果失敗或使用者取消對話方塊，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTranslator**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯的* \* pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \* pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|緩衝區長度無效|*CbNameMax*或*cbPathMax*引數小於或等於0。|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效或為 Null。|  
|ODBC_ERROR_INVALID_NAME|不正確驅動程式或翻譯工具名稱|*LpszName*引數無效。 在登錄中找不到它。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或翻譯工具安裝程式庫|無法載入 translator library。|  
|ODBC_ERROR_INVALID_OPTION|不正確交易選項|*PvOption*引數包含不正確值。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 如果 *hwndParent* 為 null，或者 *lpszName*、 *lpszPath*或 *pvOption* 是 null 指標， **SQLGetTranslator** 會傳回 FALSE。 否則，它會在下列對話方塊中顯示已安裝的轉譯程式清單。  
  
 ![[選取轉譯程式] 對話方塊](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果 *lpszName* 包含有效的翻譯工具名稱，則會選取它。 否則， \<No Translator> 就會選取。  
  
 如果使用者選擇 \<No Translator> ，就不會觸及 *lpszName*、 *lpszPath*和 *pvOption* 的內容。 **SQLGetTranslator** 會將 *pcbNameOut* 和 *pcbPathOut* 設定為0，並傳回 TRUE。  
  
 如果使用者選擇翻譯工具， **SQLGetTranslator** 會在翻譯工具的安裝 DLL 中呼叫 **ConfigTranslator** 。 如果 **ConfigTranslator** 傳回 FALSE， **SQLGetTranslator** 會返回其對話方塊。 如果 **ConfigTranslator** 傳回 true，則 **SQLGETTRANSLATOR** 會傳回 true，以及選取的翻譯工具名稱、路徑和轉譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|設定翻譯工具|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|取得翻譯屬性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定翻譯屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
