---
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
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306899"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函式
**標準**  
 引進的版本： ODBC 3.8 標準合規性： ODBC  
  
 **摘要**  
 如果可以重複使用集區中的連接， **SQLPoolConnect**會用來建立新的連接。  
  
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
 源連接控制碼。  
  
 *hDbcInfoToken*  
 源新應用程式連接要求的權杖控制碼。  
  
 *wszOutConnectString*  
 輸出已完成連接字串之緩衝區的指標。 成功連接到目標資料來源之後，此緩衝區會包含已完成的連接字串。 應用程式應該為這個緩衝區配置至少1024個字元。  
  
 如果*wszOutConnectString*為 Null， *cchConnectStringLen*仍會傳回*wszOutConnectString*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *cchConnectStringBuffer*  
 源**WszOutConnectString*緩衝區的長度（以字元為單位）。  
  
 *cchConnectStringLen*  
 輸出緩衝區的指標，要在其中傳回\* *wszOutConnectString*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*cchConnectStringBuffer*，則\* *wszOutConnectString*中已完成的連接字串會截斷為*cchConnectStringBuffer*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 類似于任何輸入驗證錯誤的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ，不同之處在于驅動程式管理員會使用 SQL_HANDLE_DBC_INFO_TOKEN 的**HandleType**和*hDbcInfoToken*的**控制碼**。  
  
## <a name="remarks"></a>備註  
 驅動程式管理員保證*hDbc*和*HDBCINFOTOKEN*的父系 HENV 控制碼相同。  
  
 與[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)不同的是，沒有任何*DriverCompletion*引數可提示使用者輸入連接資訊。 在共用案例中不允許提示對話方塊。  
  
 應用程式不應直接呼叫此函式。 支援可感知驅動程式之連接共用的 ODBC 驅動程式必須實作用此函式。  
  
 每當驅動程式傳回 SQL_ERROR 或 SQL_INVALID_HANDLE 時，驅動程式管理員會將錯誤傳回至應用程式（ [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)）。  
  
 每當驅動程式傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員就會從*hDbcInfoToken*取得診斷資訊，並將 SQL_SUCCESS_WITH_INFO 傳回至[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的應用程式。  
  
 當應用程式使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)時， *wszOutConnectString*將會是 null 緩衝區（最後三個參數全部都會設定為 Null，0，null）。 否則，驅動程式必須傳回輸出連接字串，這會傳回給應用程式的[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)調用。  
  
 包含適用于 ODBC 驅動程式開發的 sqlspi。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
