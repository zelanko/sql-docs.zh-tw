---
description: SQLForeignKeys
title: SQLForeignKeys |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6af061afe5d05b03f4b36c71ea2c222efe8e8e08
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2020
ms.locfileid: "91809555"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援串聯更新，而且會透過外部索引鍵條件約束機制刪除。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 CASCADE 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。 如果在 FOREIGN KEY 條件約束的 ON UPDATE 和/或 ON DELETE 子句上指定 NO ACTION 選項，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對 UPDATE_RULE 和/或 DELETE_RULE 資料行傳回 SQL_NO_ACTION。  
  
 當任何 **SQLForeignKeys** 參數中出現不正確值時， **SQLForeignKeys** 會在執行時傳回 SQL_SUCCESS。 當這些參數中使用無效值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 **SQLForeignKeys** 可以在靜態伺服器資料指標上執行。 嘗試在可更新的 (動態或索引鍵集) 資料指標上執行 **SQLForeignKeys** 時，SQL_SUCCESS_WITH_INFO 表示資料指標類型已經變更。  
  
 > Native Client ODBC 驅動程式支援*FKCatalogName*和*sqlforeignkeys*參數的兩部分名稱，藉此支援連結伺服器上資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQLForeignKeys 函式](../../odbc/reference/syntax/sqlforeignkeys-function.md)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
