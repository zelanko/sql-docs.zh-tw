---
description: SQLPoolConnect 函式
title: SQLPoolConnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30e2ce61baf861551e51773aea7ce6dcaf020cf6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487217"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函式
**一致性**  
 引進的版本： ODBC 3.8 標準合規性： ODBC  
  
 **總結**  
 如果集區中沒有可重複使用的連接，則會使用**SQLPoolConnect**來建立新的連線。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>引數  
 *hDbc*  
 輸出連接控制碼。  
  
 *hDbcInfoToken*  
 輸出新應用程式連接要求的權杖控制碼。  
  
 *wszOutConnectString*  
 出已完成之連接字串的緩衝區指標。 成功連接到目標資料來源時，此緩衝區包含已完成的連接字串。 應用程式應該為此緩衝區配置至少1024個字元。  
  
 如果 *wszOutConnectString* 是 Null， *cchConnectStringLen* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *wszOutConnectString*所指向的緩衝區中傳回。  
  
 *cchConnectStringBuffer*  
 輸出**WszOutConnectString* 緩衝區的長度（以字元為單位）。  
  
 *cchConnectStringLen*  
 出緩衝區的指標，此緩衝區會傳回字元總數 (不包括 null 終止字元) 可在 \* *wszOutConnectString*中傳回。 如果可傳回的字元數大於或等於*cchConnectStringBuffer*，wszOutConnectString 中已完成的連接字串 \* *wszOutConnectString*會截斷為*cchConnectStringBuffer*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 類似于任何輸入驗證錯誤的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ，不同之處在于驅動程式管理員會使用**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 驅動程式管理員保證 *hDbc* 和 *HDBCINFOTOKEN* 的父 HENV 控制碼相同。  
  
 不同于 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)，沒有 *DriverCompletion* 引數可提示使用者輸入連接資訊。 共用案例中不允許提示對話方塊。  
  
 應用程式不應該直接呼叫此函數。 支援驅動程式感知連接共用的 ODBC 驅動程式必須執行此函數。  
  
 每當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式管理員就會將錯誤傳回至 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 或 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)) 中的應用程式 (。  
  
 只要驅動程式傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員就會從 *hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回給應用程式的 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 和 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 當應用程式使用 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)時， *wszOutConnectString* 將會是 null 緩衝區 (最後三個參數都會設定為 Null、0、null) 。 否則，驅動程式必須傳回輸出連接字串，此字串將會傳回至應用程式的 [SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md) 調用。  
  
 包含用於 ODBC 驅動程式開發的 sqlspi .h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
