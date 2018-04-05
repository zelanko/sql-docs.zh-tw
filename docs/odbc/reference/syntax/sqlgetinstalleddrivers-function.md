---
title: SQLGetInstalledDrivers 函式 |Microsoft 文件
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
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64b8479b23f76c8af74be77b4f44e3bca6f8a6f6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函式
**一致性**  
 版本引進了： ODBC 1.0  
  
 **摘要**  
 **SQLGetInstalledDrivers**讀取系統資訊 [ODBC 驅動程式] 區段，並傳回一份已安裝的驅動程式的描述。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszBuf*  
 [輸出]描述安裝的驅動程式的清單。 清單結構的相關資訊，請參閱 「 註解 」。  
  
 *cbBufMax*  
 [輸入]長度*lpszBuf*。  
  
 *pcbBufOut*  
 [輸出]總位元組數 （不含 null 結束位元組） 中傳回*lpszBuf*。 如果傳回可用的位元組數目大於或等於*cbBufMax*，驅動程式描述清單中的*lpszBuf*會被截斷成*cbBufMax*減號null 結束的字元。 *PcbBufOut*引數可以是 null 指標。  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetInstalledDrivers**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式發生錯誤|發生錯誤，其中沒有特定的安裝程式錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|無效的緩衝區長度|*LpszBuf*引數為 NULL 或無效，或*cbBufMax*引數以前是小於或等於 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在登錄中找不到元件|安裝程式在登錄中找不到 [ODBC 驅動程式] 區段。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|安裝程式無法執行函式，因為記憶體不足。|  
  
## <a name="comments"></a>註解  
 Null 位元組，以終止每個驅動程式的描述，然後將整個清單以 null 位元組。 （也就是兩個 null 位元組標記清單的結尾）。如果已配置的緩衝區不足夠容納整個清單，會截斷參數清單不會發生錯誤。 如果當做傳入 null 指標，會傳回錯誤*lpszBuf*。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回的驅動程式描述和屬性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
