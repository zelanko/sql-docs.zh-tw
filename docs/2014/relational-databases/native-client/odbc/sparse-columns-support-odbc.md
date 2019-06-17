---
title: 疏鬆資料行支援 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e1583dad869860bdd2f555a354850c7f7a1198
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691952"
---
# <a name="sparse-columns-support-odbc"></a>疏鬆資料行支援 (ODBC)
  本主題將描述 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 對於疏鬆資料行的支援。 如需示範 ODBC 對於疏鬆資料行支援的範例，請參閱 <<c0> [ 具有疏鬆資料行的資料表上的呼叫 SQLColumns](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)。 如需有關疏鬆資料行的詳細資訊，請參閱 < [SQL Server Native Client 中的疏鬆資料行支援](../features/sparse-columns-support-in-sql-server-native-client.md)。  
  
## <a name="statement-metadata"></a>陳述式中繼資料  
 應用程式參數描述項 (APD) 描述項欄位和 SQL_SOPT_SS_NAME_SCOPE 陳述式屬性都會接受額外的值 SQL_SS_NAME_SCOPE_EXTENDED 和 SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET。 這些值會指定哪些資料行包含所傳回的結果集中[SQLColumns](../../native-client-odbc-api/sqlcolumns.md)。 如需有關 SQL_SOPT_SS_NAME_SCOPE 的詳細資訊，請參閱 < [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)。  
  
 新的實作資料列描述項 (IRD) (稱為 SQL_CA_SS_IS_COLUMN_SET 的唯讀 SQLSMALLINT 欄位) 可用來判斷資料行是否為 XML `column_set` 值。 SQL_CA_SS_IS_COLUMN_SET 會採用 SQL_TRUE 和 SQL_FALSE 值。  
  
## <a name="catalog-metadata"></a>目錄中繼資料  
 兩個[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]特定的資料行 （SS_IS_SPARSE 和 SS_IS_COLUMN_SET） 已新增至結果集中[SQLColumns](../../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>疏鬆資料行的 ODBC 函數支援  
 下列 ODBC 函數已經更新為支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的疏鬆資料行：  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
