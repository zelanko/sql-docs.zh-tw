---
title: SQLSetDriverConnectInfo Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f9f9ae346e58c9ea5db95386fcc80264ec82e95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537533"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函式
**合規性**  
 導入的版本：ODBC 3.81 標準合規性：ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用來設定連接字串至應用程式的連線資訊語彙基元**SQLDriverConnect**呼叫。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引數  
 *TokenHandle*  
 [輸入]語彙基元的控制代碼。  
  
 *InConnectionString*  
 [輸入]完整的連接字串 (請參閱中的 [註解] 中的語法[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))，部分連接字串或空字串。  
  
 *StringLength1*  
 [輸入]長度 **InConnectionString*，如果字串為 Unicode 或位元組如果字串為 ANSI 或 DBCS 字元。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與相同[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)與任何輸入的驗證錯誤時，不同之處在於會使用驅動程式管理員**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的並**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 只要驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤至應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或是[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 只要驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得的診斷資訊*hDbcInfoToken*，並集中的應用程式會傳回 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)並[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
