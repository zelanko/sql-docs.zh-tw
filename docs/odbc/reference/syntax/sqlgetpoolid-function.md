---
title: SQLGetPoolID 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32cc973f4dab5bde7bcedade0365d233987dda72
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303315"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 函式
**一致性**  
 版本介紹: ODBC 3.81 標準合規性: ODBC  
  
 **摘要**  
 **SQLGetPoolID**檢索池 ID。  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>引數  
 *hDbcInfoToken*  
 [輸入]包含所有連接資訊的權杖句柄。  
  
 *pPoolID*  
 【輸出]池 ID,用於標識一組可互換使用的連接(可能需要額外重置)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetPoolID**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,驅動程式管理員會使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄類型**與*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>備註  
 **SQLGetPoolID**用於獲取給定一組連接資訊的池 ID(來自**SQLSetConnectAttrForDbcInfo、SQLSetDriverConnectInfo**和**SQLSetConnectInfo)。** **SQLSetDriverConnectInfo** 此池 ID 用於標識一組可互換使用的連接(可能需要額外重置)。 池 ID 將用於標識該組連接的連接池。  
  
 每當驅動程式返回SQL_ERROR或SQL_INVALID_HANDLE時,驅動程式管理員都會將錯誤返回到應用程式(在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中)。  
  
 每當驅動程式返回SQL_SUCCESS_WITH_INFO時,驅動程式管理器將從*hDbcInfoToken*獲取診斷資訊,並在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO應用程式。  
  
 應用程式不應直接調用此功能。 支援驅動程式感知連接池的ODBC驅動程式必須實現此功能。  
  
 包括用於 ODBC 驅動程式開發的 sqlspi.h。  
  
## <a name="see-also"></a>另請參閱  
 [開發 ODBC 驅動程式](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
