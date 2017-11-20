---
title: "SQLSetConnectInfo 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e4c974a8cf4bb46f955ec8f2bae0a766f58f692
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函式
**一致性**  
 版本引進了： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用來將資料來源、 使用者識別碼和密碼設定的應用程式的連線資訊語彙基元到[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫。  
  
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
 [輸入]資料來源名稱。 資料可能會位於與程式，相同的電腦或網路上的某個地方的另一部電腦上。 如需應用程式如何選擇資料來源資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
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
 與相同[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的輸入驗證錯誤，不同之處在於會使用驅動程式管理員**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 每當驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤給應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每當驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得診斷資訊從*hDbcInfoToken*，並在應用程式傳回 SQL_SUCCESS_WITH_INFO， [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [開發中的 ODBC 驅動程式的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

