---
title: "SQLSetDriverConnectInfo 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 970fec5219fed803439fc05c3f6fe56a300617f0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函式
**一致性**  
 版本引進了： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用來設定連線資訊語彙基元中的應用程式的連接字串**SQLDriverConnect**呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引數  
 *TokenHandle*  
 [輸入]語彙基元的控制代碼。  
  
 *InConnectionString*  
 [輸入]完整連接字串 (請參閱中的 [意見] 中的語法[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))，部分連接字串或空字串。  
  
 *StringLength1*  
 [輸入]長度 **InConnectionString*，如果字串為 Unicode 或位元組如果字串為 ANSI 或 DBCS 字元。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與相同[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)與任何輸入的驗證錯誤時，不同之處在於會使用驅動程式管理員**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 每當驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤給應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每當驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得診斷資訊從*hDbcInfoToken*，並在應用程式傳回 SQL_SUCCESS_WITH_INFO， [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [開發中的 ODBC 驅動程式的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
