---
title: SQLTables |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLTables function
ms.assetid: 77b6c15c-9cf7-4019-b3f0-3d27d23ef656
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d630660d66eca46d84c8c03fa4cb45e06b3b95f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021465"
---
# <a name="sqltables"></a>SQLTables
  SQLTables 可以在靜態伺服器資料指標上執行。 嘗試在可更新的（動態或索引鍵集）資料指標上執行 SQLTables 時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 當 SQL_ALL_CATALOGS *CatalogName*參數，而且所有其他參數都包含預設值（Null 指標）時，SQLTables 會報告所有資料庫中的資料表。  
  
 若要報告可用的目錄、架構和資料表類型，SQLTables 會特別使用空字串（長度為零的位元組指標）。 空字串不是預設值 (NULL 指標)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式藉由接受*CatalogName*參數的兩部分名稱，支援連結伺服器上之資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
 SQLTables 會傳回名稱符合*TableName*且由目前使用者擁有之任何資料表的相關資訊。  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 和資料表值參數  
 當語句屬性 SQL_SOPT_SS_NAME_SCOPE 的值 SQL_SS_NAME_SCOPE_TABLE_TYPE，而不是其預設值 SQL_SS_NAME_SCOPE_TABLE 時，SQLTables 會傳回資料表類型的相關資訊。 在 SQLTables 所傳回之結果集的資料行4中，針對資料表類型傳回的 TABLE_TYPE 值為 TABLE 類型。 如需 SQL_SOPT_SS_NAME_SCOPE 的詳細資訊，請參閱[SQLSetStmtAttr](sqlsetstmtattr.md)。  
  
 資料表、檢視與同義字共用與資料表類型所使用之命名空間不同的一般命名空間。 雖然不可能擁有具有相同名稱的資料表和檢視，但是在相同的目錄和結構描述中，可能擁有具有相同名稱的資料表和資料表類型。  
  
 如需資料表值參數的詳細資訊，請參閱[ODBC&#41;&#40;的資料表值參數](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
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
 [SQLTables 函式](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
