---
title: SQLSetConnectInfo 函式 |Microsoft Docs
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
ms.openlocfilehash: e5d8087e7672dd331d0b078cea4930be7582a026
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68092999"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函式
**標準**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**是用來將資料來源、使用者識別碼和密碼設定為應用程式[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)呼叫的連接資訊 token。  
  
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
 *TokenHandle*  
 源權杖控制碼。  
  
 *ServerName*  
 源資料來源名稱。 資料可能位於與程式相同的電腦上，或位於網路上某處的另一部電腦上。 如需應用程式如何選擇資料來源的詳細資訊，請參閱[選擇資料來源或驅動程式](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 源**ServerName*的長度（以字元為單位）。  
  
 *UserName*  
 源使用者識別碼。  
  
 *NameLength2*  
 源**UserName*的長度（以字元為單位）。  
  
 *驗證*  
 源驗證字串（通常是密碼）。  
  
 *NameLength3*  
 源**驗證*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與輸入驗證錯誤的[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)相同，不同之處在于驅動程式管理員會使用 SQL_HANDLE_DBC_INFO_TOKEN 的**HandleType**和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 每當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式管理員會將錯誤傳回至應用程式（ [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)）。  
  
 每當驅動程式傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員就會從*hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回至[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的應用程式。  
  
 應用程式不應直接呼叫此函式。 支援可感知驅動程式之連接共用的 ODBC 驅動程式必須實作用此函式。  
  
 包含適用于 ODBC 驅動程式開發的 sqlspi。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連線集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
