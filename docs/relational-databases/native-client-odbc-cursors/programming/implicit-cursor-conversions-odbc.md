---
title: 隱含資料指標轉換 (ODBC) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-cursors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d6d03a04c6c46941dc205d791029de5b63acaff0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="implicit-cursor-conversions-odbc"></a>隱含資料指標轉換 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  應用程式可以要求透過資料指標類型[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) ，然後執行伺服端資料指標要求的型別不支援的 SQL 陳述式。 呼叫**SQLExecute**或**SQLExecDirect**傳回 SQL_SUCCESS_WITH_INFO 和**SQLGetDiagRec**傳回：  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 應用程式可以判斷哪些類型的資料指標正在使用藉由呼叫**SQLGetStmtOption**設定為 SQL_CURSOR_TYPE。 資料指標類型轉換只適用於一個陳述式。 下一步 **SQLExecDirect**或**SQLExecute**都是使用原始陳述式資料指標設定。  
  
## <a name="see-also"></a>另請參閱  
 [資料指標程式設計詳細&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
