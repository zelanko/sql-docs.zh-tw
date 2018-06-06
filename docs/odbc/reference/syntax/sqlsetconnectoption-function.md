---
title: SQLSetConnectOption 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 965a563620dc95720602b03091dd38507cfa1e08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函式
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： 已被取代  
  
 **摘要**  
 在 ODBC 3 *.x*，ODBC 2.0 函式**SQLSetConnectOption**已被取代**SQLSetConnectAttr**。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]  
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 2 *.x*應用程式使用 ODBC 3 *.x*驅動程式，請參閱[對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>備註  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式將在 64 位元作業系統上執行。  
  
> [!NOTE]  
>  不支援屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE ODBC 3.8 中導入**SQLSetConnectOption**。 使用連接控制代碼上的非同步作業的應用程式必須使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
