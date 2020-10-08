---
description: SQLColumnPrivileges
title: SQLColumnPrivileges |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e85edde7aaba43dab43d486e5b615a27f50bc19e
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809894"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLColumnPrivileges** 會傳回值，SQL_SUCCESS*CatalogName*、 *SchemaName*、 *TableName*或 *ColumnName* 參數的值是否存在。 當這些參數中使用無效值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 **SQLColumnPrivileges** 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 **SQLColumnPrivileges** 時，將會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已經變更。  
  
 > Native Client ODBC 驅動程式會藉由接受*CatalogName*參數的兩部分名稱，來支援連結伺服器上資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumnPrivileges 函式](../../odbc/reference/syntax/sqlcolumnprivileges-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
