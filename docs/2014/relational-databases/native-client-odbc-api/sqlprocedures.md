---
title: SQLProcedures |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a7855016bf7c0dec86775cc6a1a289d0b317031
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417717"
---
# <a name="sqlprocedures"></a>SQLProcedures
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預存程序都會傳回值。 **SQLProcedures**會針對結果集資料行 PROCEDURE_TYPE 報告 sql_pt_function。  
  
 **SQLProcedures**或是否有值存在都會傳回 SQL_SUCCESS *CatalogName、 SchemaName*或是*ProcName*參數。 **SQLFetch**無效的值用於這些參數時，會傳回 sql_no_data 為止。  
  
 **SQLProcedures**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLProcedures**可更新的 （動態或索引鍵集） 資料指標上將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 **SQLProcedures**傳回名稱符合任何程序的相關資訊*ProcName*而且由目前的使用者，或目前使用者已被授與 VIEW DEFINITION 權限可以執行。  
  
## <a name="see-also"></a>另請參閱  
 [SQLProcedures 函數](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
