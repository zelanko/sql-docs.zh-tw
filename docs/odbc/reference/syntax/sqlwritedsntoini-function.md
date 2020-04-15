---
title: SQLwriteSntoini 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bb141c8f54c49ca3a5c6fc4bc15d434f91795c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286958"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函式
**一致性**  
 版本介紹: ODBC 1.0  
  
 **摘要**  
 **SQLWriteDSNToini**向系統資訊添加了數據源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>引數  
 *lpszDSN*  
 [輸入]要添加的數據源的名稱。  
  
 *lpszDriver*  
 [輸入]向使用者而不是物理驅動程式名稱顯示的驅動程式描述(通常是關聯的 DBMS 的名稱)。  
  
## <a name="returns"></a>傳回值  
 如果成功,則函數返回 TRUE,如果失敗,則返回 FALSE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLWriteDSNToini**傳回 FALSE 時,可以透過呼叫**SQL 安裝程式錯誤**獲得關聯的*\*pfErrorCode*值。 下表列出了**SQL 安裝程式錯誤**可以返回的*\*pfErrorCode*值,並在此函數的上下文中解釋了每個值。  
  
|*\*pfError 碼*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般安裝程式錯誤|發生沒有特定安裝程式錯誤的錯誤。|  
|ODBC_ERROR_INVALID_DSN|不合法的 DSN|*lpszDSN*參數包含一個對 DSN 無效的字串。|  
|ODBC_ERROR_INVALID_NAME|不合法的驅動程式或翻譯者名稱|*lpszDriver*參數無效。|  
|ODBC_ERROR_REQUEST_FAILED|要求失敗|安裝程式未能在註冊表中創建 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|記憶體不足|由於記憶體不足,安裝程式無法執行該功能。|  
  
## <a name="comments"></a>註解  
 **SQLWriteDSNToI**將資料源添加到系統資訊的 [ODBC 資料源] 部分。 然後,它為資料源創建一個規範節,並添加一個關鍵字 (**驅動程式**), 其值為驅動程式 DLL 的名稱。 如果數據源規範部分已存在,則**SQLWriteDSNToi 會在**創建新節之前刪除舊節。  
  
 此函數的調用方必須向系統資訊的數據源規範部分添加任何特定於驅動程式的關鍵字和值。  
  
 如果數據源的名稱為"預設 **",SQLWriteDSNToi**還會在系統資訊中創建預設驅動程序規範部分。  
  
 此函數應僅從設置 DLL 調用。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|新增、修改或移除資料來源|[設定DSN(](../../../odbc/reference/syntax/configdsn-function.md)在安裝程式 DLL 中 )|  
|新增、修改或移除資料來源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|從系統資訊中移除資料來源名稱|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
