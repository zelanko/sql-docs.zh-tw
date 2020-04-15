---
title: 稀疏列支援 (ODBC) |微軟文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2dd987453202af2d7761e70193f8a0968f4ad38d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303684"
---
# <a name="sparse-columns-support-odbc"></a>疏鬆資料行支援 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題將描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 對於疏鬆資料行的支援。 有關展示 ODBC 支援稀疏列的範例,請參閱[在具有稀疏列的表上調用 SQLColumns](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 有關稀疏列的詳細資訊,請參閱[SQL Server 本機客戶端中的稀疏列支援](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>陳述式中繼資料  
 應用程式參數描述項 (APD) 描述項欄位和 SQL_SOPT_SS_NAME_SCOPE 陳述式屬性都會接受額外的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 這些值指定[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)返回的結果集中包含哪些列。 有關SQL_SOPT_SS_NAME_SCOPE的詳細資訊,請參閱[SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新的實現行描述符 (IRD) 是一個唯讀 SQLSMALLINT 欄位,稱為 SQL_CA_SS_IS_COLUMN_SET,可用於確定列是否為 XML **column_set**值。 SQL_CA_SS_IS_COLUMN_SET 會採用 SQL_TRUE 和 SQL_FALSE 值。  
  
## <a name="catalog-metadata"></a>目錄中繼資料  
 兩[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]個特定的列(SS_IS_SPARSE和SS_IS_COLUMN_SET)已添加到[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)的結果集中。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>疏鬆資料行的 ODBC 函數支援  
 下列 ODBC 函數已經更新為支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的疏鬆資料行：  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
