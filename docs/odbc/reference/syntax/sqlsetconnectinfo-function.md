---
title: SQLSetConnectInfo Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88af314c1cca5ef2d7cdbdb2b5e555b81d02be01
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287304"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函式
**合規性**  
 導入的版本：ODBC 3.81 標準合規性：ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用來設定資料來源、 使用者識別碼和密碼到應用程式的連線資訊語彙基元[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>引數  
 *TokenHandle*  
 [輸入]語彙基元的控制代碼。  
  
 *ServerName*  
 [輸入]資料來源名稱。 資料可能位於程式，在同一部電腦或網路上的某個位置的另一部電腦上。 如需應用程式如何選擇資料來源資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [輸入]長度 **ServerName*以字元為單位。  
  
 *UserName*  
 [輸入]使用者識別碼。  
  
 *NameLength2*  
 [輸入]長度 **UserName*以字元為單位。  
  
 *驗證*  
 [輸入]驗證字串 （通常是密碼）。  
  
 *NameLength3*  
 [輸入]長度 **驗證*以字元為單位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與相同[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的輸入驗證錯誤，不同之處在於會使用驅動程式管理員**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的並**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 只要驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤至應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或是[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 只要驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得的診斷資訊*hDbcInfoToken*，並集中的應用程式會傳回 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)並[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
