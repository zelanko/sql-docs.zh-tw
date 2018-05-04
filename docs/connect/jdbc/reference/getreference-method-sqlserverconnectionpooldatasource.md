---
title: getReference 方法 (SQLServerConnectionPoolDataSource) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8c48de91-de55-4f25-a5f1-36a8e8c4629e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55ad660a69af8d178fa7bce61e43f27ca29d4f49
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getreference-method-sqlserverconnectionpooldatasource"></a>getReference 方法 (SQLServerConnectionPoolDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將參考傳回給這[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>傳回值  
 參考物件。  
  
## <a name="remarks"></a>備註  
 這個 getReference 方法是由 javax.naming.Referenceable 介面中的 getReference 方法指定。 它會覆寫[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)方法[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
