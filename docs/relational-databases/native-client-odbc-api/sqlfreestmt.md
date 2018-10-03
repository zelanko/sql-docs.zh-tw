---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9555c5fd335abcf4069c4ca9241bbade8f71771
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844202"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  通常   
      **SQLFreeStmt**不建議使用在 ODBC 3.0 和更新版本。 不過如果應用程式需要重複使用陳述式仍建議您使用**SQLFreeStmt**具有**SQL_RESET_PARAMS**並**SQL_UNBIND**選項)。 您也可以使用[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)， [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)， [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)， [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)，和[SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)來取代或重複的函式**SQLFreeStmt**應該改為使用它們。  
  
 一般情況下，它是更有效率的方式重複使用比要卸除它們，並配置新的陳述式。 不過在某些情況下，例如陳述式中，重複使用 SQLFreeStmt 仍然必須使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLFreeStmt 函數](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
