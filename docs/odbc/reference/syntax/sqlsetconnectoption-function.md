---
title: SQLSet連接選項功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectOption
helpviewer_keywords:
- SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263b15cb75fb5c0c7c1d7aa630a8da171b9765a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301593"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函式
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 已棄用  
  
 **摘要**  
 在 ODBC 3 *.x*中,ODBC 2.0 函數**SQLSetConnectOption**已被**SQLSetConnectAttr**替換。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC 2 *.x*應用程式使用 ODBC 3 *.x*驅動程式時的詳細資訊,請參閱[映射已棄用函數](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)"。  
  
## <a name="remarks"></a>備註  
 如果應用程式將在 64 位元作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
> [!NOTE]  
>  **SQLSetConnectOption**不支援在 ODBC 3.8 中引入的屬性SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接句柄上使用非同步操作的應用程式必須使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
