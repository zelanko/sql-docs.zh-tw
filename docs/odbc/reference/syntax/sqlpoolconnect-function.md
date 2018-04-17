---
title: SQLPoolConnect 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 130c39d4aab986b5053192d2fe2c548e89ccef2e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函式
**一致性**  
 版本引進了： ODBC 3.8 標準相容性： ODBC  
  
 **摘要**  
 **SQLPoolConnect**用來建立新的連接，如果沒有連接集區中的可以重複使用。  
  
## <a name="syntax"></a>語法  
  
```  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>引數  
 *hDbc*  
 [輸入]連接控制代碼。  
  
 *hDbcInfoToken*  
 [輸入]新的應用程式連接要求的語彙基元的控制代碼。  
  
 *wszOutConnectString*  
 [輸出]已完成的連接字串緩衝區的指標。 目標資料來源的連接成功，這個緩衝區會包含完整的連接字串。 應用程式應該為這個緩衝區配置至少 1024 個字元。  
  
 如果*wszOutConnectString*是 NULL， *cchConnectStringLen*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回中緩衝區所指*wszOutConnectString*。  
  
 *cchConnectStringBuffer*  
 [輸入]長度 **wszOutConnectString*緩衝區，以字元為單位。  
  
 *cchConnectStringLen*  
 [輸出]這是要傳回的總字元數 （不包括 null 結束字元） 中的緩衝區指標可用來傳回中\* *wszOutConnectString*。 可傳回的字元數目是否大於或等於*cchConnectStringBuffer*，完成連接字串中的\* *wszOutConnectString*會被截斷成*cchConnectStringBuffer*減去 null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO，SQL_ERROR，或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 類似於[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)任何輸入驗證錯誤時，不同之處在於會使用驅動程式管理員**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**處理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>備註  
 驅動程式管理員可確保 HENV 處理的父系*hDbc*和*hDbcInfoToken*都相同。  
  
 不同於[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)，沒有任何*DriverCompletion*引數，以提示使用者輸入連接資訊。 共用的案例中，不允許提示對話方塊。  
  
 應用程式不應該直接呼叫此函式。 支援可感知驅動程式的連接集區的 ODBC 驅動程式必須實作此函式。  
  
 每當驅動程式會傳回 SQL_ERROR 或 SQL_INVALID_HANDLE，驅動程式管理員會傳回錯誤給應用程式 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每當驅動程式會傳回 SQL_SUCCESS_WITH_INFO，驅動程式管理員會取得診斷資訊從*hDbcInfoToken*，並在應用程式傳回 SQL_SUCCESS_WITH_INFO， [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 當應用程式使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)， *wszOutConnectString*將 NULL 緩衝區 （最後三個參數將所有設定為 NULL、 0 或 NULL）。 否則，此驅動程式必須傳回輸出連接字串，它會傳回給應用程式的[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)呼叫。  
  
 包含 sqlspi.h ODBC 驅動程式開發。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [可感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
