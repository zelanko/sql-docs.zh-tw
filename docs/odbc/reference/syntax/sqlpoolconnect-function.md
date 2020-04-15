---
title: SQLPool連接功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306899"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函式
**一致性**  
 版本介紹: ODBC 3.8 標準合規性: ODBC  
  
 **摘要**  
 如果池中無法重用任何連接,**則 SQLPoolConnect**用於創建新連接。  
  
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
 *赫德布*  
 [輸入]連接句柄。  
  
 *hDbcInfoToken*  
 [輸入]新應用程式連接請求的權杖句柄。  
  
 *wszOutConnectString*  
 【輸出]指向已完成連接字串的緩衝區。 成功連接到目標資料來源後,此緩衝區包含已完成的連接字串。 應用程式應為此緩衝區分配至少 1,024 個字元。  
  
 如果*wszOutConnectString*為*NULL,cchConnectStringLen*仍將傳回可用在*wszOutConnectString*指向的緩衝區中傳回的字元總數(不包括字元資料的空終止字元)。  
  
 *cchConnectString緩衝區*  
 [輸入]**wszOutConnectString*緩衝區的長度(以字元表示)。  
  
 *cchConnectStringLen*  
 【輸出]指向一個緩衝區的指標,其中返回可在\**wszOutConnectString*中返回的字元總數(不包括空終止字元)。 如果可供返回的字元數大於或等於*cchConnectStringBuffer,*\**則 wszOutConnectString*中已完成的連接字串將被截斷為*cchConnectStringBuffer*減去空終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 與[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)的任何輸入驗證錯誤類似,只不過驅動程式管理員會使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄類型**與*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>備註  
 驅動程式管理員保證 hDbc 和*hDbcInfoToken*的父 HENV 句柄相同。 *hDbc*  
  
 與[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)不同,沒有*驅動程式完成*參數來提示使用者輸入連接資訊。 在池化方案中不允許提示對話方塊。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 每當驅動程式返回SQL_ERROR或SQL_INVALID_HANDLE時,驅動程式管理員都會將錯誤返回到應用程式(在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中)。  
  
 每當驅動程式返回SQL_SUCCESS_WITH_INFO時,驅動程式管理器將從*hDbcInfoToken*獲取診斷資訊,並在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO應用程式。  
  
 當應用程式使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)時 *,wszOutConnectString*將是一個 NULL 緩衝區(最後三個參數將全部設置為 NULL、0、NULL)。 否則,驅動程式必須返回輸出連接字串,該字串將返回到應用程式的[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)調用。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
