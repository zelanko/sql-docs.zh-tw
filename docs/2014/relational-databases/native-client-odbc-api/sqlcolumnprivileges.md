---
title: SQLColumnPrivileges |Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 35bd61c12933dac25ac90d8b56afb0e17b44d3ab
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706328"
---
# <a name="sqlcolumnprivileges"></a>SQLColumnPrivileges
  **SQLColumnPrivileges**會傳回 SQL_SUCCESS*CatalogName*、 *SchemaName*、 *TableName*或*ColumnName*參數的值是否存在。 當這些參數中使用了不正確值時， **SQLFetch**會傳回 SQL_NO_DATA。  
  
 **SQLColumnPrivileges**可以在靜態伺服器資料指標上執行。 嘗試在可更新的（動態或索引鍵集）資料指標上執行**SQLColumnPrivileges**時，將會傳回 SQL_SUCCESS_WITH_INFO，表示資料指標類型已變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式藉由接受*CatalogName*參數的兩部分名稱，支援連結伺服器上之資料表的報告資訊： *Linked_Server_Name. Catalog_Name*。  
  
## <a name="see-also"></a>另請參閱  
 [SQLColumnPrivileges 函式](https://go.microsoft.com/fwlink/?LinkId=59335)   
 [ODBC API 實作詳細資料](odbc-api-implementation-details.md)  
  
  
