---
title: ConfigTranslator 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306029"
---
# <a name="configtranslator-function"></a>ConfigTranslator 函式
**標準**  
 引進的版本： ODBC 2。0  
  
 **摘要**  
 **ConfigTranslator**會傳回翻譯工具的預設轉譯選項。 它可以位於 translator DLL 或個別的安裝程式 DLL 中。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>引數  
 *hwndParent*  
 源父視窗控制碼。 如果控制碼為 null，函數不會顯示任何對話方塊。  
  
 *pvOption*  
 輸出32位的轉譯選項。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**ConfigTranslator**傳回 FALSE 時，會呼叫**SQLPostInstallerError**來將相關聯* \*的 pfErrorCode*值張貼到安裝程式錯誤緩衝區，並可透過呼叫**SQLInstallerError**來取得。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|不正確視窗控制碼|*HwndParent*引數無效或為 Null。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或 translator 特定的錯誤|驅動程式特定的錯誤，其中沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPostInstallerError**函式中的*SzError*引數應該包含驅動程式特定的錯誤訊息。|  
|ODBC_ERROR_INVALID_OPTION|不正確轉譯選項|*PvOption*引數包含不正確值。|  
  
## <a name="comments"></a>評價  
 如果翻譯工具僅支援單一翻譯選項，則**ConfigTranslator**會傳回 TRUE，並將*pvOption*設定為32位選項。 否則，它會決定要使用的預設轉譯選項。 **ConfigTranslator**可以顯示對話方塊，供使用者選取預設的轉譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得翻譯選項|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|選取翻譯工具|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|設定翻譯選項|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
