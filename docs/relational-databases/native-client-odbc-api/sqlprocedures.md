---
description: SQLProcedures
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5fc316c908b5de2e2fab906bbe80c1ed52caaec6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485000"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures** SQL_PT_FUNCTION 結果集資料行的報表 PROCEDURE_TYPE。  
  
 **SQLProcedures** 會傳回值 *，SQL_SUCCESS CatalogName、SchemaName* 或 *ProcName* 參數是否有值存在。 當這些參數中使用無效值時， **SQLFetch** 會傳回 SQL_NO_DATA。  
  
 **SQLProcedures** 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 **SQLProcedures** ，將會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已經變更。  
  
 **SQLProcedures** 會傳回其名稱符合 *ProcName* 且可由目前使用者執行，或是目前使用者已被授與 VIEW DEFINITION 許可權之任何程式的相關資訊。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedures 函式](../../odbc/reference/syntax/sqlprocedures-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
