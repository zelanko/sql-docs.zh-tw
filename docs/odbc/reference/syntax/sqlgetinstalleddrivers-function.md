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
manager: craigg
ms.openlocfilehash: 0ff675a184ea0804988972ef10e9a383cdd45230
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537208"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函式
**合規性**  
 導入的版本：ODBC 1.0  
  
 **摘要**  
 **SQLGetInstalledDrivers**讀取系統資訊 [ODBC 驅動程式] 區段，並傳回一份已安裝的驅動程式的描述。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszBuf*  
 [輸出]描述安裝的驅動程式的清單。 清單結構的相關資訊，請參閱 「 註解。 」  
  
 *cbBufMax*  
 [輸入]長度*lpszBuf*。  
  
 *pcbBufOut*  
 [輸出]總位元組數 （不含終止 null 位元組） 中傳回*lpszBuf*。 傳回可用的位元組數目是否大於或等於*cbBufMax*，清單中的驅動程式說明*lpszBuf*會被截斷成*cbBufMax*減去null 結束字元。 *PcbBufOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetInstalledDrivers**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的安裝程式錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszBuf*引數為 NULL 或無效，或有*cbBufMax*引數小於或等於 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到的元件|安裝程式在登錄中找不到 [ODBC 驅動程式] 區段。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足，安裝程式無法執行函式。|  
  
## <a name="comments"></a>註解  
 每個驅動程式的描述會終止具有 null 位元組，並將整個清單結尾 null 位元組。 （也就是兩個 null 位元組標記清單的結尾）。如果配置的緩衝區不大到足以保留整個清單，清單會截斷不會發生錯誤。 如果是 null 指標，會當做傳遞中，會傳回錯誤*lpszBuf*。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回的驅動程式描述和屬性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
