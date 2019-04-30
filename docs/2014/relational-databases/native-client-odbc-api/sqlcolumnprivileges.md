---
title: SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 737ace72f201f3abe192393b1a1cc3747f5774e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067754"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges**或是否有值存在都會傳回 SQL_SUCCESS*CatalogName*， *SchemaName*， *TableName*，或*ColumnName*參數。 **SQLFetch**無效的值用於這些參數時，會傳回 sql_no_data 為止。  
  
 **SQLColumnPrivileges**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLColumnPrivileges**上可更新的 （動態或索引鍵集） 資料指標會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援的報告資訊的連結伺服器上的資料表所接受的兩部分名稱*CatalogName*參數：*Linked_Server_Name.Catalog_Name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumnPrivileges 函數](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
