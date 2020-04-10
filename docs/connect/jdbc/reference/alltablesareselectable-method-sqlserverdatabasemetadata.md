---
title: allTablesAreSelectable 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allTablesAreSelectable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: eb340450-45a7-49c8-84bc-1b9dd5ee842f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4fbd5a1d132bdb1e0d661e05968709ed604006d9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922912"
---
# <a name="alltablesareselectable-method-sqlserverdatabasemetadata"></a>allTablesAreSelectable 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出目前使用者是否有權限可以在 SELECT 陳述式中使用由 [getTables](../../../connect/jdbc/reference/gettables-method-sqlserverdatabasemetadata.md) 方法傳回的所有資料表。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean allTablesAreSelectable()  
```  
  
## <a name="return-value"></a>傳回值  
 如果使用者有權限可使用所有資料表，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 allTablesAreSelectable 方法是由 java.sql.DatabaseMetaData 介面中的 allTablesAreSelectable 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
