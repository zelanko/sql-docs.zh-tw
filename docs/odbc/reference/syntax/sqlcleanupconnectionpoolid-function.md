---
title: "SQLCleanupConnectionPoolID 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 155df975e89008090e0ec2d5c856c74fe85ddfdd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函式
**一致性**  
 版本引進了： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知集區識別碼逾時的驅動程式。集區識別碼可以逾時，只要在該集區識別碼相關聯的集區中的所有連接都已逾時。請參閱[Microsoft Data Access Components 中共用](http://msdn.microsoft.com/library/ms810829.aspx)如需有關連接逾時。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 [輸入]環境控制代碼的集區。  
  
 *PoolID*  
 [輸入]逾時的集區識別碼相關聯的集區。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從傳回的診斷資訊**SQLCleanupConnectionPoolID**。  
  
 應用程式無法接收驅動程式所傳回的錯誤訊息。  
  
## <a name="remarks"></a>備註  
 **SQLCleanupConnectionPoolID**可以呼叫任何時候，但是驅動程式管理員可保證沒有其他執行緒的呼叫同時**SQLGetPoolID**和任何其他執行緒正在同時呼叫**SQLRateConnection**和**SQLPoolConnect**與連接資訊的語彙基元，指派給該集區識別碼。 因此，驅動程式必須確定此函式是安全執行緒。  
  
 驅動程式可以清除集區識別碼相關聯的資源  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>請參閱＜  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
