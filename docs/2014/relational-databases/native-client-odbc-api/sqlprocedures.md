---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046675"
---
# <a name="sqlprocedures"></a>SQLProcedures
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures**會針對結果集資料行 PROCEDURE_TYPE 報告 sql_pt_function。  
  
 **SQLProcedures**或是否有值存在都會傳回 SQL_SUCCESS *CatalogName、 SchemaName*或是*ProcName*參數。 **SQLFetch**無效的值用於這些參數時，會傳回 sql_no_data 為止。  
  
 **SQLProcedures**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLProcedures**可更新的 （動態或索引鍵集） 資料指標上將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 **SQLProcedures**傳回名稱符合任何程序的相關資訊*ProcName*而且由目前的使用者，或目前使用者已被授與 VIEW DEFINITION 權限可以執行。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedures 函數](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
