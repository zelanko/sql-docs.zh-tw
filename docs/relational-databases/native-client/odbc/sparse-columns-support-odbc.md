---
description: 疏鬆資料行支援 (ODBC)
title: " (ODBC) 的稀疏資料行支援 |Microsoft Docs"
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6015682353cbe2145aad22024392ffa0a4c65ff2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97418330"
---
# <a name="sparse-columns-support-odbc"></a>疏鬆資料行支援 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  本主題將描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 對於疏鬆資料行的支援。 如需示範 ODBC 支援稀疏資料行的範例，請參閱在 [含有稀疏資料行的資料表上呼叫 SQLColumns](../../../relational-databases/native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 如需有關稀疏資料行的詳細資訊，請參閱 [SQL Server Native Client 中的稀疏資料行支援](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>陳述式中繼資料  
 應用程式參數描述項 (APD) 描述項欄位和 SQL_SOPT_SS_NAME_SCOPE 陳述式屬性都會接受額外的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 這些值會指定要將哪些資料行包含在 [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)所傳回的結果集中。 如需 SQL_SOPT_SS_NAME_SCOPE 的詳細資訊，請參閱 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新的實值資料列描述項 (IRD) （稱為 SQL_CA_SS_IS_COLUMN_SET 的唯讀 SQLSMALLINT 欄位），可用來判斷資料行是否為 XML **column_set** 值。 SQL_CA_SS_IS_COLUMN_SET 會採用 SQL_TRUE 和 SQL_FALSE 值。  
  
## <a name="catalog-metadata"></a>目錄中繼資料  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SS_IS_SPARSE 和 SS_IS_COLUMN_SET) 的兩個特定資料行已加入至[SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)的結果集。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>疏鬆資料行的 ODBC 函數支援  
 下列 ODBC 函數已經更新為支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的疏鬆資料行：  
  
-   [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../../relational-databases/native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
