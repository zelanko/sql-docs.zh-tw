---
title: getPooledConnection 方法 （) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aad6c325-3398-462c-aa6e-201dc89fa5ef
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7f70e710b03e0af9e91001da20afc97c3d839d5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838073"
---
# <a name="getpooledconnection-method-"></a>getPooledConnection 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試建立可用來當做共用連接的實體資料庫連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.sql.PooledConnection getPooledConnection()  
```  
  
## <a name="return-value"></a>傳回值  
 A [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getPooledConnection 方法是由 javax.sql.ConnectionPoolDataSource 介面中 getPooledConnection 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
