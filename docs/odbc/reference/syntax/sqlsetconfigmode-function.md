---
title: SQLSetConfigMode 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a10ec8f8fa6ef2b0e310680f58252f98628ff045
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62656056"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函式
**合規性**  
 導入的版本：ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**設定指出列出資料來源名稱值的 Odbc.ini 項目中的系統資訊的組態模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *wConfigMode*  
 [輸入]安裝程式組態模式 （請參閱 「 註解 」）。 中的值*wConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConfigMode**會傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的此函式。  
  
|*\*pfErrorCode*|錯誤|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無效的參數順序|*WConfigMode* ODBC_USER_DSN、 ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN 不包含引數。|  
  
## <a name="comments"></a>註解  
 此函式用來設定列出資料來源名稱值的 Odbc.ini 項目所在的系統資訊。 如果*wConfigMode* ODBC_USER_DSN，資料來源名稱是 「 使用者 DSN，和函式會讀取 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果是 ODBC_SYSTEM_DSN，DSN 為系統 DSN 和函式會讀取在 HKEY_LOCAL_MACHINE 的 Odbc.ini 項目。 如果是 ODBC_BOTH_DSN，HKEY_CURRENT_USER 時嘗試，而且若失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
 此函式不會影響**SQLCreateDataSource**並**SQLDriverConnect**。 設定模式必須進行設定時藉由呼叫驅動程式會從登錄讀取**SQLGetPrivateProfileString**或藉由呼叫寫入登錄**SQLWritePrivateProfileString**。 呼叫**SQLGetPrivateProfileString**並**SQLWritePrivateProfileString**知道哪一個部分要處理的登錄中使用設定模式。  
  
> [!CAUTION]  
>  **SQLSetConfigMode**僅時必要的; 如果模式不正確設定，ODBC 安裝程式可能無法正確運作，應該呼叫。  
  
 **SQLSetConfigMode**直接登錄修改的組態模式。 這是除了修改組態模式下所呼叫的程序**SQLConfigDataSource**。 呼叫**SQLConfigDataSource**設定組態模式來區分使用者與系統 Dsn，修改資料來源名稱時。 傳回前, **SQLConfigDataSource**將組態模式重設 BOTHDSN。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|擷取組態模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
