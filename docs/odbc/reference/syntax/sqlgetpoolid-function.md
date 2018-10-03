---
title: SQLGetPoolID 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39b3d3d1ecdc21acee8b238f56cede0a59146bd2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740056"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 函式
**合規性**  
 版本導入： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLGetPoolID**擷取集區識別碼。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>引數  
 *hDbcInfoToken*  
 [輸入]包含所有的連接資訊的權杖控制代碼。  
  
 *pPoolID*  
 [輸出]集區識別碼，這用來識別的一組可交換使用的連接 （可能需要額外的重設）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetPoolID**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，驅動程式管理員會使用**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的並**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 **SQLGetPoolID**用來取得提供一組連接資訊的集區識別碼 (從**SQLSetConnectAttrForDbcInfo**， **SQLSetDriverConnectInfo**，和**SQLSetConnectInfo**)。 此集區識別碼用來識別的一組可交換使用的連接 （可能需要額外的重設）。 集區識別碼將用來識別該群組的連線的連接集區中。  
  
 只要驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤至應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或是[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 只要驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得的診斷資訊*hDbcInfoToken*，並集中的應用程式會傳回 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)並[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
