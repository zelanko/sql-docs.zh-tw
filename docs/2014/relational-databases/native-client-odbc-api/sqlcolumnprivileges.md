---
title: SQLColumnPrivileges |Microsoft Docs
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
- SQLColumnPrivileges function
ms.assetid: c78acd4e-8668-4abc-9bc9-6ad381965863
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6462213fddd646c1461f0975dc89b151c192de3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425727"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges**或是否有值存在都會傳回 SQL_SUCCESS*CatalogName*， *SchemaName*， *TableName*，或*ColumnName*參數。 **SQLFetch**無效的值用於這些參數時，會傳回 sql_no_data 為止。  
  
 **SQLColumnPrivileges**可以在靜態伺服器資料指標上執行。 嘗試執行**SQLColumnPrivileges**上可更新的 （動態或索引鍵集） 資料指標會傳回 SQL_SUCCESS_WITH_INFO，指出資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援的報告資訊的連結伺服器上的資料表所接受的兩部分名稱*CatalogName*參數： *Linked_Server_Name.Catalog_Name*.  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumnPrivileges 函數](http://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
