---
title: 隱含游標轉換 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ced726893b0f287db6b1fec7c8d16c6b844eea2b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298378"
---
# <a name="implicit-cursor-conversions-odbc"></a>隱含資料指標轉換 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  應用程式可以通過[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)請求游標類型,然後執行請求類型的伺服器游標不支援的 SQL 語句。 SQLExecute 或**SQLExecDirect** **的**呼叫傳回SQL_SUCCESS_WITH_INFO **SQLGetDiagRec**傳回:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 應用程式可以通過將**SQLGetStmtOption**設置為SQL_CURSOR_TYPE來確定現在使用的游標類型。 資料指標類型轉換只適用於一個陳述式。 下一個**SQLExecDirect**或**SQLExecute**將使用原始語句游標設置完成。  
  
## <a name="see-also"></a>另請參閱  
 [游標程式設計詳細資訊&#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
