---
title: SQLSetConnectOption 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d22d1bf5fc3d01bf62afd2da6b3ebbc2bb0289
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742264"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：已被取代  
  
 **摘要**  
 在 ODBC 3 *.x*，ODBC 2.0 函式**SQLSetConnectOption**已被取代**SQLSetConnectAttr**。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 2 *.x*應用程式使用 ODBC 3 *.x*驅動程式，請參閱[對應已被取代的函式](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>備註  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式會在 64 位元作業系統上執行。  
  
> [!NOTE]  
>  不支援屬性符合 ODBC 3.8 中導入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLSetConnectOption**。 使用連接控制代碼上的非同步作業的應用程式必須使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
