---
title: SQLGet 安裝驅動程式功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303325"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函式
**一致性**  
 版本介紹: ODBC 1.0  
  
 **摘要**  
 **SQLGet安裝驅動程式**讀取系統資訊的 [ODBC 驅動程式] 部分,並返回已安裝驅動程式的說明清單。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>引數  
 *lpszBuf*  
 【輸出]已安裝驅動程式的說明清單。 有關清單結構的資訊,請參閱"註釋"。  
  
 *cbBufMax*  
 [輸入]*lpszBuf*的長度 。  
  
 *多布布夫*  
 【輸出]以*lpszBuf*返回的位元組總數(不包括空終止位元組)。 如果可用於返回的位元組數大於或等於*cbBufMax,**則 lpszBuf*中的驅動程式描述清單將截斷為*cbBufMax*減去空終止字元。 *pcbBufOut*參數可以是空指標。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGet 安裝驅動程式**返回 FALSE 時,可以通過調用**SQL 安裝程序獲取**關聯的*\*pfError 代碼*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_BUFF_LEN|不合法緩衝區長度|*lpszBuf*參數為 NULL 或無效,或者*cbBufMax*參數小於或等於 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|註冊表中找不到元件|安裝程式在註冊表中找不到 [ODBC 驅動程式] 部分。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 每個驅動程式描述都用空位元組終止,整個清單用空位元節終止。 (即,兩個空位元組標記清單的末尾。如果分配的緩衝區不夠大,無法容納整個清單,則清單將被截斷,而不會出錯。 如果空指標作為*lpszBuf*傳入,則返回錯誤。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回驅動程式描述與屬性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
