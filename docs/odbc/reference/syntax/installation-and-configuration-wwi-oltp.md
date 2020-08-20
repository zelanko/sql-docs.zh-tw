---
description: SQLSetDriverConnectInfo 函式
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
ms.openlocfilehash: 21538fa93328790ad8173e5193ba377b0744d964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461250"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函式
**一致性**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **總結**  
 **SQLSetDriverConnectInfo** 可用來將連接字串設定為應用程式 **SQLDriverConnect** 呼叫的連接資訊權杖。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引數  
 *TokenHandle*  
 輸出權杖控制碼。  
  
 *InConnectionString*  
 輸出完整的連接字串 (在 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)) 、部分連接字串或空字串的「批註」中看到語法。  
  
 *StringLength1*  
 輸出如果字串為 Unicode，則 **InConnectionString*的長度（以字元為單位），如果字串為 ANSI 或 DBCS，則為位元組。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與任何輸入驗證錯誤相關的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)相同，不同之處在于驅動程式管理員會使用 SQL_HANDLE_DBC_INFO_TOKEN 的**HandleType**和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 每當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式管理員就會將錯誤傳回至 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 或 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)) 中的應用程式 (。  
  
 只要驅動程式傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員就會從 *hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回給應用程式的 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 和 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函數。 支援驅動程式感知連接共用的 ODBC 驅動程式必須執行此函數。  
  
 包含用於 ODBC 驅動程式開發的 sqlspi .h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
