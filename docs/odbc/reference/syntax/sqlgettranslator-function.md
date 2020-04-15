---
title: SQLGet 翻譯器功能 |微軟文件
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
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303269"
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLGet 轉換器**顯示一個對話框,用戶可以從該對話框中選擇譯員。  
  
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
 *hwnd 家長*  
 [輸入]父視窗句柄。  
  
 *lpsz名稱*  
 [輸入/輸出]系統資訊中的轉換器名稱。  
  
 *cbNameMax*  
 [輸入]*lpszName*緩衝區的最大長度。  
  
 *pcbNameOut*  
 [輸入/輸出]以*lpszName*透過或傳回的位元組總數(不包括空終止位元組)。 如果可用於返回的位元組數大於或等於*cbNameMax,**則 lpszName*中的轉換器名稱將被截斷為*cbNameMax*減去 null 終止字元。 *pcbNameOut*參數可以是空指標。  
  
 *lpszPath*  
 【輸出]翻譯 DLL 的完整路徑。  
  
 *cbPathMax*  
 [輸入]*lpszPath*緩衝區的最大長度。  
  
 *多巴帕路*  
 【輸出]在*lpszPath*中返回的位元組總數(不包括空終止位元組)。 如果可用於返回的位元組數大於或等於*cbPathMax,**則 lpszPath*中的轉換 DLL 路徑將截斷為*cbPathMax*減去 null 終止字元。 *pcbPathOut*參數可以是空指標。  
  
 *pvOption*  
 [輸出] 32 位元轉換選項。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數將返回 TRUE;如果失敗或使用者取消對話框,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGet 轉換器**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式獲取**關聯的*\*pfError 程式*。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*cbNameMax*或*cbPathMax*參數小於或等於 0。|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效或 NULL。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszName*參數無效。 在註冊表中找不到它。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|無法載入驅動程式或轉換器設定庫|無法載入轉換器庫。|  
|ODBC_ERROR_INVALID_OPTION|不合法的事務選項|*pvOption*參數包含無效值。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 如果*hwndParent*為空,或者如果*lpszName、lpszPath*或*pvOption*是空指標,**則 SQLGet 轉換器**傳回 FALSE。 *lpszPath* 否則,它將在下面的對話框中顯示已安裝的譯員的清單。  
  
 ![[選取轉譯程式] 對話方塊](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 如果*lpszName*包含有效的轉換器名稱,則選中該名稱。 否則,\<則不選擇"翻譯>。  
  
 \<如果用戶選擇「無翻譯器>,則不會觸摸*lpszName、lpszPath*和*pvOption*的內容。 *lpszPath* **SQLGet 轉換器**將*pcbNameOut*和*pcbPathOut*設定為 0,並返回 TRUE。  
  
 如果使用者選擇翻譯**器,SQLGet 轉換器**在譯器的設定 DLL 中呼叫**設定翻譯器**。 如果**配置轉換器**返回**FALSE,SQLGet 轉換器**將傳回到其對話框。 如果**配置轉換器**返回**TRUE,SQLGet 轉換器**將返回 TRUE,以及所選的轉換器名稱、路徑和翻譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置譯員|[設定轉換器](../../../odbc/reference/syntax/configtranslator-function.md)|  
|取得翻譯屬性|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|設定轉換屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
