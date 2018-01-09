---
title: "SQLProcedures |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23a0c1de61959b3a69766b6554f4c20694dea208
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures**針對結果集資料行 PROCEDURE_TYPE 報告 sql_pt_function Q。  
  
 **SQLProcedures**是否存在的值都會傳回 SQL_SUCCESS *CatalogName、 SchemaName*或*ProcName*參數。 **SQLFetch**這些參數中使用無效值時，傳回 sql_no_data 為止。  
  
 **SQLProcedures**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLProcedures**可更新的 （動態或索引鍵集） 資料指標上將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已經變更。  
  
 **SQLProcedures**傳回名稱符合任何程序的相關資訊*ProcName*而且由目前的使用者，或目前使用者已被授與 VIEW DEFINITION 權限可以執行。  
  
## <a name="see-also"></a>請參閱  
 [SQLProcedures 函數](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
