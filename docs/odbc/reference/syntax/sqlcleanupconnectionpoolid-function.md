---
title: SQLCleanup 連接池 ID 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301318"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLCleanupConnectionPoolID**通知驅動程式池 ID 已超時。每當與該池 ID 關聯的池中的所有連接超時時,池 ID 都可以超時。有關連接逾時的詳細資訊,請參閱[Microsoft 資料存取元件中的池](https://msdn.microsoft.com/library/ms810829.aspx)。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>引數  
 *環境處理*  
 [輸入]池的環境句柄。  
  
 *池識別碼*  
 [輸入]與超時的池 ID 關聯的池。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 驅動程式管理員不會處理從**SQLCleanupConnection 池 ID**返回的診斷資訊。  
  
 應用程式無法接收驅動程式返回的錯誤訊息。  
  
## <a name="remarks"></a>備註  
 **SQLCleanupConnectionPoolID**可以隨時呼叫,但驅動程式管理員保證沒有其他線程同時呼叫**SQLGetPoolID,** 並且沒有其他線程同時使用該池 ID 分配的連接資訊權碼呼叫**SQLRateConnection**和**SQLPoolConnect。** 因此,驅動程式必須確保此函數是線程安全的。  
  
 驅動程式可以清理與池 ID 關聯的資源。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
