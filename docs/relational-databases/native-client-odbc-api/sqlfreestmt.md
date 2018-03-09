---
title: SQLFreeStmt | Microsoft Docs
ms.custom: 
ms.date: 11/23/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a198bb508f07bd16278df4784d4c5705bbdf8f9e
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通常   
      **SQLFreeStmt**建議您不要在 ODBC 3.0 和更新版本。 但是如果重複使用陳述式的應用程式需要您應該仍然使用**SQLFreeStmt**與**SQL_RESET_PARAMS**和**SQL_UNBIND**選項)。 您也可以使用[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)， [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)， [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)，和[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)取代或重複的函式**SQLFreeStmt** ，應該改用它們。  
  
 一般情況下，會重複使用比卸除它們並配置新的陳述式更有效率。 不過在某些情況下，重複使用的陳述式，例如 SQLFreeStmt 仍然必須使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeStmt 函數](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
