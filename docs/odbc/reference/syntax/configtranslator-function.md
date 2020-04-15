---
title: 設定翻譯功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306029"
---
# <a name="configtranslator-function"></a>ConfigTranslator 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **配置轉換器**返回翻譯器的預設翻譯選項。 它可以在轉換器 DLL 或單獨的設置 DLL 中。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>引數  
 *hwnd 家長*  
 [輸入]父視窗句柄。 如果句柄為空,則函數將不會顯示任何對話方塊。  
  
 *pvOption*  
 【輸出]32 位元轉換選項。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**配置轉換器**返回 FALSE 時,透過呼叫**SQLPost 安裝程式錯誤**將關聯的*\*pfError 程式*碼值發布到安裝程式錯誤緩衝區,並且可以透過呼叫**SQL 安裝程式錯誤**獲得。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|無效的視窗句柄|*hwnd 父參數*無效或 NULL。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驅動程式或轉換器特定錯誤|驅動程式特定的錯誤,沒有定義的 ODBC 安裝程式錯誤。 呼叫**SQLPost 安裝程式錯誤**函數時 *,SzError*參數應包含特定於驅動程式的錯誤訊息。|  
|ODBC_ERROR_INVALID_OPTION|不合法選項|*pvOption*參數包含無效值。|  
  
## <a name="comments"></a>註解  
 如果轉換器僅支援單個平移選項,**則設定轉換器**將返回 TRUE 並將*pvOption*設置到 32 位元選項。 否則,它確定要使用的默認轉換選項。 **設定翻譯器**可以顯示一個對話框,用戶可以選擇預設翻譯選項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得翻譯選項|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|選擇譯員|[SQLGet 轉換器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|設定翻譯選項|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
