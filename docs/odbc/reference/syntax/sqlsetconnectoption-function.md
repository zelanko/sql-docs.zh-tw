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
ms.openlocfilehash: b429e499cccaad553236b4ebee78374c69c7c4dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093016"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **摘要**  
 在 ODBC 3.x*中，odbc*2.0 函數**SQLSetConnectOption**已由**SQLSetConnectAttr**取代。 如需詳細資訊，請參閱 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  如需 ODBC 2.x 應用程式使用 ODBC 3.x*驅動程式時*，驅動程式管理員將此函式對應至哪個內容的** 詳細資訊，請參閱[對應](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)已被取代的函式。  
  
## <a name="remarks"></a>備註  
 如果您的應用程式將在64位作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
> [!NOTE]  
>  **SQLSetConnectOption**不支援 ODBC 3.8 中引進的屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接控制碼上使用非同步作業的應用程式必須使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
