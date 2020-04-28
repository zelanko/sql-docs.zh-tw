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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a74a92cc05ecd41e99ff87642c7fe3ee527e0c98
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301318"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函式
**標準**  
 引進的版本： ODBC 3.81 標準合規性： ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**會通知驅動程式，集區識別碼已超時。當集區中與該集區識別碼相關聯的所有連線都已超時時，集區識別碼可能會超時。如需連接逾時的詳細資訊，請參閱[Microsoft 資料存取元件中](https://msdn.microsoft.com/library/ms810829.aspx)的共用。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>引數  
 *EnvironmentHandle*  
 源集區的環境控制碼。  
  
 *PoolID*  
 源與已計時的集區識別碼相關聯的集區。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從**SQLCleanupConnectionPoolID**傳回的診斷資訊。  
  
 應用程式無法接收驅動程式所傳回的錯誤訊息。  
  
## <a name="remarks"></a>備註  
 您可以隨時呼叫**SQLCleanupConnectionPoolID** ，但驅動程式管理員保證沒有其他執行緒同時呼叫**SQLGetPoolID** ，而且沒有其他執行緒同時呼叫**SQLRateConnection**和**SQLPOOLCONNECT** ，以及使用該集區識別碼指派的連接資訊權杖。 因此，驅動程式必須確保此函式具備執行緒安全。  
  
 驅動程式可以清除與集區識別碼相關聯的資源。  
  
 應用程式不應直接呼叫此函式。 支援可感知驅動程式之連接共用的 ODBC 驅動程式必須實作用此函式。  
  
 包含適用于 ODBC 驅動程式開發的 sqlspi。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
