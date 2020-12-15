---
description: SQLTables
title: SQLTables |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44ec790c3a372bfd2dae8f22cbdc6f50608c9426
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465049"
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  SQLTables 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 SQLTables 時，將會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已經變更。  
  
 當 SQL_ALL_CATALOGS *CatalogName* 參數，而且所有其他參數都包含 (Null 指標) 的預設值時，SQLTables 會報告所有資料庫中的資料表。  
  
 若要報告可用的目錄、架構和資料表類型，SQLTables 會)  (零長度的位元組指標，以特殊使用空字串。 空字串不是預設值 (NULL 指標)。  
  
 > Native Client ODBC 驅動程式會藉由接受 *CatalogName* 參數的兩部分名稱，來支援連結伺服器上資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
 SQLTables 會傳回名稱符合 *TableName* 且由目前使用者所擁有之任何資料表的相關資訊。  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 和資料表值參數  
 當語句屬性 SQL_SOPT_SS_NAME_SCOPE 具有 SQL_SS_NAME_SCOPE_TABLE_TYPE 的值（而不是其預設值 SQL_SS_NAME_SCOPE_TABLE）時，SQLTables 會傳回資料表類型的相關資訊。 在 SQLTables 所傳回之結果集的資料行4中，針對資料表類型所傳回的 TABLE_TYPE 值是資料表類型。 如需 SQL_SOPT_SS_NAME_SCOPE 的詳細資訊，請參閱 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 資料表、檢視與同義字共用與資料表類型所使用之命名空間不同的一般命名空間。 雖然不可能擁有具有相同名稱的資料表和檢視，但是在相同的目錄和結構描述中，可能擁有具有相同名稱的資料表和資料表類型。  
  
 如需資料表值參數的詳細資訊，請參閱 [&#40;ODBC&#41;的資料表值參數 ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
## <a name="example"></a>範例  
  
```  
// Get a list of all tables in the current database.  
SQLTables(hstmt, NULL, 0, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of all tables in all databases.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, NULL, 0, NULL, 0, NULL,0);  
  
// Get a list of databases on the current connection's server.  
SQLTables(hstmt, (SQLCHAR*) "%", SQL_NTS, (SQLCHAR*)"", 0, (SQLCHAR*)"",  
    0, NULL, 0);  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQLTables 函式](../../odbc/reference/syntax/sqltables-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
