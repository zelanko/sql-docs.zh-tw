---
title: SQLSetConnectInfo 功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301849"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用於將資料源、使用者 ID 和密碼設定為應用程式的[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫的連接資訊權杖中。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
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
 *權杖*  
 [輸入]令牌句柄。  
  
 *ServerName*  
 [輸入]數據源名稱。 數據可能位於與程式相同的電腦上,或者位於網路上的另一台電腦上。 關於應用程式如何選擇資料來源的資訊,請參考[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [輸入]長度 = 以字元表示*伺服器名稱*。  
  
 *使用者*  
 [輸入]用戶識別碼。  
  
 *名稱長度2*  
 [輸入]長度 =*字元中的使用者名稱*。  
  
 *驗證*  
 [輸入]身份驗證字串(通常是密碼)。  
  
 *名稱長度3*  
 [輸入]長度 =*字元認證*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)一樣,用於輸入驗證錯誤,只不過驅動程式管理員使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄類型**與*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>備註  
 每當驅動程式返回SQL_ERROR或SQL_INVALID_HANDLE時,驅動程式管理員都會將錯誤返回到應用程式(在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中)。  
  
 每當驅動程式返回SQL_SUCCESS_WITH_INFO時,驅動程式管理器將從*hDbcInfoToken*獲取診斷資訊,並在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO應用程式。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
