---
title: SQLTransact 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a4f1da36a7c233e9a1b5832ee83e86a5c1f77d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287078"
---
# <a name="sqltransact-function"></a>SQLTransact 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性：已淘汰  
  
 **摘要**  
 在 ODBC 3.x*中，odbc* *2.x 函數* **SQLTransact**已由**SQLEndTran**取代。 如需詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  **SQLTransact**不支援在 ODBC 3.8 中引進的屬性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 在連接控制碼上使用非同步作業的應用程式必須使用**SQLEndTran**。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
