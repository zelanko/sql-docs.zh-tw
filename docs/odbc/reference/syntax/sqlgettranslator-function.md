---
title: "SQLGetTranslator 函式 |Microsoft 文件"
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
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76bc8c85e923c792e87c13c2ca7f490c7273d975
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函式
**一致性**  
 版本引進了： ODBC 2.0  
  
 **摘要**  
 **SQLGetTranslator**顯示的對話方塊，使用者可以從中選取的轉譯器。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]父視窗控制代碼。  
  
 *lpszName*  
 [輸入/輸出]系統資訊從轉譯程式的名稱。  
  
 *cbNameMax*  
 [輸入]最大長度*lpszName*緩衝區。  
  
 *pcbNameOut*  
 [輸入/輸出]（不含 null 結束位元組） 的位元組總數傳遞或傳回*lpszName*。 如果傳回可用的位元組數目大於或等於*cbNameMax*中的轉譯器名稱*lpszName*會被截斷成*cbNameMax*減號null 結束的字元。 *PcbNameOut*引數可以是 null 指標。  
  
 *lpszPath*  
 [輸出]轉譯 DLL 的完整路徑。  
  
 *cbPathMax*  
 [輸入]最大長度*lpszPath*緩衝區。  
  
 *pcbPathOut*  
 [輸出]總位元組數 （不含 null 結束位元組） 中傳回*lpszPath*。 如果可用來傳回的位元組數目大於或等於*cbPathMax*中的轉譯 DLL 路徑*lpszPath*會被截斷成*cbPathMax*減號null 結束的字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *pvOption*  
 [輸出] 32 位元轉譯選項。  
  
## <a name="returns"></a>傳回值  
 如果它是成功，則為 FALSE 如果失敗，或使用者取消對話方塊中，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTranslator**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*CbNameMax*或*cbPathMax*引數以前是小於或等於 0。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數以前是無效或為 NULL。|  
|ODBC_ERROR_INVALID_NAME|驅動程式或轉譯器名稱無效|*LpszName*引數無效。 它不在登錄中。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯程式的安裝程式庫|無法載入轉譯程式庫。|  
|ODBC_ERROR_INVALID_OPTION|無效的交易選項|*PvOption*引數包含無效的值。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 如果*hwndParent*為 null 或*lpszName*， *lpszPath*，或*pvOption*為 null 指標， **SQLGetTranslator**會傳回 FALSE。 否則，它會顯示已安裝的轉譯器的清單中出現下列對話方塊。  
  
 ![選取的轉譯程式對話方塊](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含有效的轉譯程式的名稱，選取它。 否則，\<否轉譯程式 > 已選取。  
  
 如果使用者選擇\<否轉譯程式 >，內容*lpszName*， *lpszPath*，和*pvOption*不接觸。 **SQLGetTranslator**設定*pcbNameOut*和*pcbPathOut*為 0，並傳回 TRUE。  
  
 如果使用者選擇的轉譯器， **SQLGetTranslator**呼叫**ConfigTranslator**轉譯程式的安裝程式 DLL 中。 如果**ConfigTranslator**會傳回 FALSE， **SQLGetTranslator**傳回它的對話方塊。 如果**ConfigTranslator**會傳回 TRUE， **SQLGetTranslator**傳回 TRUE，以及選取的轉譯程式的名稱、 路徑和轉譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|設定轉譯器|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|取得轉譯屬性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定轉譯屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
