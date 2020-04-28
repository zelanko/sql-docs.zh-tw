---
title: SQLSetDriverConnectInfo 函式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298795"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函式
**標準**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**是用來將連接字串設定為應用程式**SQLDriverConnect**呼叫的連接資訊 token。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引數  
 *TokenHandle*  
 源權杖控制碼。  
  
 *InConnectionString*  
 源完整的連接字串（請參閱[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的「批註」中的語法）、部分連接字串或空字串。  
  
 *StringLength1*  
 源**InConnectionString*的長度（如果字串是 Unicode，則以字元為單位）; 如果 STRING 為 ANSI 或 DBCS，則為位元組。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與與任何輸入驗證錯誤相關的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)相同，不同之處在于驅動程式管理員會使用 SQL_HANDLE_DBC_INFO_TOKEN 的**HandleType**和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 每當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式管理員會將錯誤傳回至應用程式（ [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)）。  
  
 每當驅動程式傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員就會從*hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回至[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的應用程式。  
  
 應用程式不應直接呼叫此函式。 支援可感知驅動程式之連接共用的 ODBC 驅動程式必須實作用此函式。  
  
 包含適用于 ODBC 驅動程式開發的 sqlspi。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
