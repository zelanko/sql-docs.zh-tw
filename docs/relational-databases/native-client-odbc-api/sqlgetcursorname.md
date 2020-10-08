---
description: SQLGetCursorName
title: SQLGetCursorName |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b957389a627fc32da6b72dc56b215e0fc62cd8ee
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810550"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  如果應用程式未指定資料指標名稱，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驅動程式會在資料指標產生時為應用程式產生一個資料指標名稱。 應用程式可以使用 **SQLGetCursorName** 來取得定位 UPDATE 和 DELETE 子句的驅動程式定義資料指標名稱。 應用程式不需要呼叫 **SQLSetCursorName** 來利用定位的資料動作陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [SQLGetCursorName 函式](../../odbc/reference/syntax/sqlgetcursorname-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
