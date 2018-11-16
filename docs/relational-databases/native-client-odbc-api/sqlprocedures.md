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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bd400221a3e199deb50ac8cb384984dc64bca83
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674467"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures**會針對結果集資料行 PROCEDURE_TYPE 報告 sql_pt_function。  
  
 **SQLProcedures**或是否有值存在都會傳回 SQL_SUCCESS *CatalogName、 SchemaName*或是*ProcName*參數。 **SQLFetch**無效的值用於這些參數時，會傳回 sql_no_data 為止。  
  
 **SQLProcedures**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLProcedures**可更新的 （動態或索引鍵集） 資料指標上將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 **SQLProcedures**傳回名稱符合任何程序的相關資訊*ProcName*而且由目前的使用者，或目前使用者已被授與 VIEW DEFINITION 權限可以執行。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedures 函數](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
