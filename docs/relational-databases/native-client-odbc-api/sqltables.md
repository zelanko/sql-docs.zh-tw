---
title: SQLTables |微軟文件
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f3fa2b053c41facba7d608b2352772abd3ff103
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291736"
---
# <a name="sqltables"></a>SQLTables
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQLTables 可以在靜態伺服器游標上執行。 嘗試在可上升(動態或鍵集)游標上執行 SQLTables 將返回SQL_SUCCESS_WITH_INFO指示游標類型已更改。  
  
 當*目錄名稱*參數SQL_ALL_CATALOGS並且所有其他參數包含預設值(NULL指標)時,SQLTables 會報告所有資料庫的表。  
  
 要報告可用的目錄、架構和表類型,SQLTables 會特別使用空字串(零長度字節指標)。 空字串不是預設值 (NULL 指標)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式通過接受*目錄名稱*參數的兩部分名稱 *(Linked_Server_Name.Catalog_Name)* 支援報告連結伺服器上的表的資訊。  
  
 SQLTables 傳回有關名稱與*表格Name*符合且歸目前使用者所有的任何表的資訊。  
  
## <a name="sqltables-and-table-valued-parameters"></a>SQLTables 和資料表值參數  
 當語句屬性SQL_SOPT_SS_NAME_SCOPE具有值SQL_SS_NAME_SCOPE_TABLE_TYPE,而不是其預設值SQL_SS_NAME_SCOPE_TABLE時,SQLTables 將返回有關表類型的資訊。 SQLTables 傳回的結果集的第 4 列中傳回的表類型的TABLE_TYPE值是 TABLE TYPE。 有關SQL_SOPT_SS_NAME_SCOPE的詳細資訊,請參閱[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 資料表、檢視與同義字共用與資料表類型所使用之命名空間不同的一般命名空間。 雖然不可能擁有具有相同名稱的資料表和檢視，但是在相同的目錄和結構描述中，可能擁有具有相同名稱的資料表和資料表類型。  
  
 有關表值參數的詳細資訊,請參閱[&#40;ODBC&#41;的表值參數](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)。  
  
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
 [SQLTables 函數](https://go.microsoft.com/fwlink/?LinkId=59374)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
