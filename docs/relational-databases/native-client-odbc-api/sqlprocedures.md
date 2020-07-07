---
title: SQLProcedures |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 41d7f8058b753991186a9bbadc1b7badc02ef29d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011129"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures** PROCEDURE_TYPE 結果集資料行的報表 SQL_PT_FUNCTION。  
  
 **SQLProcedures**會傳回 SQL_SUCCESS *CatalogName、SchemaName*或*ProcName*參數的值是否存在。 當這些參數中使用了不正確值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 **SQLProcedures**可以在靜態伺服器資料指標上執行。 嘗試在可更新的（動態或索引鍵集）資料指標上執行**SQLProcedures**時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 **SQLProcedures**會傳回名稱符合*ProcName*且可由目前使用者執行，或是目前使用者已被授與 VIEW DEFINITION 許可權之任何程式的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedures 函式](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
