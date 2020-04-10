---
title: getReference 方法 (SQLServerConnectionPoolDataSource)| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8c48de91-de55-4f25-a5f1-36a8e8c4629e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55df93254976bcef4d7346267f4f4da0884e1cdc
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925103"
---
# <a name="getreference-method-sqlserverconnectionpooldatasource"></a>getReference 方法 (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回這個 [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) 物件的參考。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>傳回值  
 Reference 物件。  
  
## <a name="remarks"></a>備註  
 這個 getReference 方法是由 javax.naming.Referenceable 介面中的 getReference 方法指定。 它會覆寫 [SQLServerDataSource](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md) 類別的 [getReference](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
