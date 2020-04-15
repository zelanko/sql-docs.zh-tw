---
title: SQLSetDriverConnectInfo 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10336475e39598161126c13771ad822de0d5f7d8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298795"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用於將連接字串設定為應用程式的**SQLDriverConnect**呼叫的連線資訊權杖。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引數  
 *權杖*  
 [輸入]令牌句柄。  
  
 *連接字串*  
 [輸入]完整的連接字串(請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的「註釋」中的語法)、部分連接字串或空字串。  
  
 *字串長度1*  
 [輸入]如果字串為 Unicode,則長度 =*連接字串*,或字串為 ANSI 或 DBCS 的位元組。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與與任何輸入驗證錯誤相關的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)相同,只不過驅動程式管理員會使用 SQL_HANDLE_DBC_INFO_TOKEN的**句柄類型**與*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>備註  
 每當驅動程式返回SQL_ERROR或SQL_INVALID_HANDLE時,驅動程式管理員都會將錯誤返回到應用程式(在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中)。  
  
 每當驅動程式返回SQL_SUCCESS_WITH_INFO時,驅動程式管理器將從*hDbcInfoToken*獲取診斷資訊,並在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO應用程式。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
