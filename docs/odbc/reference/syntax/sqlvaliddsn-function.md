---
title: SQLValidDSN 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286968"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函式
**一致性**  
 版本介紹: ODBC 2.0  
  
 **摘要**  
 **SQLValidDSN**在將名稱添加到系統資訊之前檢查數據源名稱的長度和有效性。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要檢查的數據源名稱。  
  
## <a name="returns"></a>傳回值  
 如果數據源名稱有效,則函數將返回 TRUE。 如果數據源名稱無效或函數調用失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLValidDSN**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 僅當函數調用失敗時,才返回*\*pfErrorCode,* 而不是由於數據源名稱無效而返回 FALSE。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLValidDSN**由驅動程式的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)呼叫,以檢查資料來源名稱的長度和資料原始名稱中各個字元的有效性。 它檢查名稱的長度是否大於 sqlext.h 中定義的SQL_MAX_DSN_LENGTH。 (資料來源名稱的長度也由[SQLWriteDSNToini 檢查](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)。**SQLValidDSN**檢查資料來源名稱中是否包含以下任何無效字元:  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除資料來源|[設定DSN(](../../../odbc/reference/syntax/configdsn-function.md)在安裝程式 DLL 中 )|  
|新增、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|將資料來源名稱寫入系統資訊|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
