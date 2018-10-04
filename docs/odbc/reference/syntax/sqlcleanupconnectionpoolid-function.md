---
title: SQLCleanupConnectionPoolID 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dc2552c848b691346c57a0191f9c9200bad4523
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666166"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函式
**合規性**  
 版本導入： ODBC 3.81 標準相容性： ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知逾時的集區識別碼的驅動程式。集區識別碼可以逾時，每當該集區識別碼相關聯的集區中的所有連線都已逾時。請參閱[Microsoft Data Access Components 中的共用](http://msdn.microsoft.com/library/ms810829.aspx)取得的連接逾時的詳細資訊。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 [輸入]集區的環境控制代碼。  
  
 *PoolID*  
 [輸入]逾時的集區識別碼相關聯的集區。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從傳回的診斷資訊**SQLCleanupConnectionPoolID**。  
  
 應用程式無法接收驅動程式所傳回的錯誤訊息。  
  
## <a name="remarks"></a>備註  
 **SQLCleanupConnectionPoolID**可呼叫在任何時間，但驅動程式管理員可保證沒有其他執行緒正在同時呼叫**SQLGetPoolID**並沒有任何其他執行緒同時呼叫**SQLRateConnection**並**SQLPoolConnect**與連接資訊的語彙基元，指派該集區識別碼。 因此，驅動程式必須確定此函式是安全執行緒。  
  
 驅動程式可以清除集區識別碼相關聯的資源  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接共用的 ODBC 驅動程式必須實作此函式。  
  
 包含 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
