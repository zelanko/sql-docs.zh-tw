---
title: SQLGetInstalledDrivers 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e7b079e2b66f4e1ba7b3233a6aaa20cd9908a67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061518"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函式
**標準**  
 引進的版本： ODBC 1。0  
  
 **摘要**  
 **SQLGetInstalledDrivers**會讀取系統資訊的 [ODBC 驅動程式] 區段，並傳回已安裝驅動程式的描述清單。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszBuf*  
 輸出已安裝之驅動程式的描述清單。 如需清單結構的詳細資訊，請參閱「批註」。  
  
 *cbBufMax*  
 源*LpszBuf*的長度。  
  
 *pcbBufOut*  
 輸出*LpszBuf*中傳回的位元組總數（不包括 null 終止位元組）。 如果可傳回的位元組數目大於或等於*cbBufMax*， *lpszBuf*中的驅動程式描述清單會截斷為*cbBufMax*減去 null 終止字元。 *PcbBufOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，函式會傳回 TRUE，如果失敗，則傳回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetInstalledDrivers**傳回 FALSE 時，可以藉由呼叫**SQLInstallerError**來取得相關聯* \*的 pfErrorCode*值。 下表列出可由**SQLInstallerError**傳回的* \*pfErrorCode*值，並在此函式的內容中說明每一個值。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生錯誤，但沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不正確緩衝區長度|*LpszBuf*引數為 Null 或無效，或*cbBufMax*引數小於或等於0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式在登錄中找不到 [ODBC 驅動程式] 區段。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|因為記憶體不足，所以安裝程式無法執行函數。|  
  
## <a name="comments"></a>註解  
 每個驅動程式描述都會以 null 位元組結束，而整個清單會以 null 位元組結束。 （也就是兩個 null 位元組會標示清單結尾）。如果配置的緩衝區不夠大，無法保存整個清單，則會截斷清單而不會發生錯誤。 如果以*lpszBuf*傳入 null 指標，則會傳回錯誤。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回驅動程式描述和屬性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
