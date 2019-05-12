---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 948fc36da520777812c02e6e5d52a423eb9cc288
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536541"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函式
**合規性**  
 導入的版本：ODBC 2.0  
  
 **摘要**  
 **SQLGetTranslator**會顯示一個對話方塊，使用者可以從中選取的轉譯器。  
  
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
 [輸入]父視窗控制代碼。  
  
 *lpszName*  
 [輸入/輸出]系統資訊從轉譯程式的名稱。  
  
 *cbNameMax*  
 [輸入]最大長度*lpszName*緩衝區。  
  
 *pcbNameOut*  
 [輸入/輸出]（不含終止 null 位元組） 的位元組總數傳遞或傳回*lpszName*。 傳回可用的位元組數目是否大於或等於*cbNameMax*中的轉譯程式名稱*lpszName*會被截斷成*cbNameMax*減號null 結束字元。 *PcbNameOut*引數可以是 null 指標。  
  
 *lpszPath*  
 [輸出]轉譯 DLL 的完整路徑。  
  
 *cbPathMax*  
 [輸入]最大長度*lpszPath*緩衝區。  
  
 *pcbPathOut*  
 [輸出]總位元組數 （不含終止 null 位元組） 中傳回*lpszPath*。 傳回可用的位元組數目是否大於或等於*cbPathMax*中的轉譯 DLL 路徑*lpszPath*會被截斷成*cbPathMax*減號null 結束字元。 *PcbPathOut*引數可以是 null 指標。  
  
 *pvOption*  
 [輸出] 32 位元轉譯選項。  
  
## <a name="returns"></a>傳回值  
 如果它是成功，則為 FALSE 如果失敗，或如果使用者取消 [] 對話方塊中，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTranslator**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*CbNameMax*或是*cbPathMax*引數小於或等於 0。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗控制代碼|*HwndParent*引數是無效或為 NULL。|  
|ODBC_ERROR_INVALID_NAME|無效的驅動程式或轉譯器名稱|*LpszName*引數無效。 它找不到在登錄中。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉譯器的安裝程式庫|無法載入轉譯器程式庫。|  
|ODBC_ERROR_INVALID_OPTION|無效的交易選項|*PvOption*引數包含無效的值。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 如果*hwndParent*是 null 或者*lpszName*， *lpszPath*，或*pvOption*為 null 指標， **SQLGetTranslator**會傳回 FALSE。 否則，在下列對話方塊中顯示已安裝的轉譯器清單。  
  
 ![選取的轉譯程式對話方塊](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含有效的轉譯器名稱，加以選取。 否則， \<No 轉譯器 > 已選取。  
  
 如果使用者選擇\<No 轉譯器 >，內容*lpszName*， *lpszPath*，和*pvOption*不觸及。 **SQLGetTranslator**設定*pcbNameOut*並*pcbPathOut*為 0，則傳回 TRUE。  
  
 如果使用者選擇 translator **SQLGetTranslator**呼叫**ConfigTranslator**轉譯程式的安裝程式 DLL 中。 如果**ConfigTranslator**會傳回 FALSE， **SQLGetTranslator**傳回給它的對話方塊。 如果**ConfigTranslator**會傳回 TRUE， **SQLGetTranslator**傳回 TRUE，以及選取的轉譯器的名稱、 路徑和轉譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|設定轉譯器|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|取得翻譯的屬性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定翻譯的屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
