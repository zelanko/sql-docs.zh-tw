---
title: SQLSetConfigMode 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30236bf71edd6dd96ac28fcdc603fd8d27081a6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 函式
**一致性**  
 版本引進了： ODBC 3.0  
  
 **摘要**  
 **SQLSetConfigMode**設定指出列出 DSN 值的 Odbc.ini 項目中的系統資訊的組態模式。  
  
## <a name="syntax"></a>語法  
  
```  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引數  
 *wConfigMode*  
 [輸入]安裝程式組態模式 （請參閱 [意見]）。 中的值*wConfigMode*可以是：  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>傳回值  
 如果成功，FALSE 如果失敗，則函數會傳回 TRUE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConfigMode**傳回 FALSE，相關聯 *\*pfErrorCode*可以取得值，藉由呼叫**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以傳回的值**SQLInstallerError** ，並說明每個內容中的這個函式。  
  
|*\*pfErrorCode*|錯誤|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無效的參數順序|*WConfigMode* ODBC_USER_DSN、 ODBC_SYSTEM_DSN 或 ODBC_BOTH_DSN 不包含引數。|  
  
## <a name="comments"></a>註解  
 此函式用來設定列出 DSN 值的 Odbc.ini 項目所在的系統資訊。 如果*wConfigMode* ODBC_USER_DSN，DSN 為使用者 DSN 而且函式會讀取在 HKEY_CURRENT_USER 中的 Odbc.ini 項目。 如果是 ODBC_SYSTEM_DSN，DSN 為系統 DSN，並從 Odbc.ini 中的項目 HKEY_LOCAL_MACHINE 的函式讀取。 如果是 ODBC_BOTH_DSN，HKEY_CURRENT_USER 時嘗試，而且若失敗，則會使用 HKEY_LOCAL_MACHINE。  
  
 此函式不會影響**SQLCreateDataSource**和**SQLDriverConnect**。 將設定模式已藉由呼叫驅動程式會從登錄讀取設定**SQLGetPrivateProfileString**或寫入登錄中藉由呼叫**SQLWritePrivateProfileString**。 呼叫**SQLGetPrivateProfileString**和**SQLWritePrivateProfileString**知道哪一個部分上操作登錄的使用將設定模式。  
  
> [!CAUTION]  
>  **SQLSetConfigMode**僅 ODBC 安裝程式時所需的; 如果模式不正確設定，可能無法正常運作，應該呼叫。  
  
 **SQLSetConfigMode**組態模式的直接登錄修改了。 這是修改組態模式下所呼叫的程序除了**SQLConfigDataSource**。 呼叫**SQLConfigDataSource**設定來區分使用者和系統 Dsn，修改 DSN 時將設定模式。 在傳回時之前, **SQLConfigDataSource** BOTHDSN 重設為將設定模式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|建立資料來源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|擷取組態模式|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
