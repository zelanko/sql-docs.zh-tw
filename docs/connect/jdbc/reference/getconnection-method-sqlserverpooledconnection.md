---
title: getConnection 方法 (SQLServerPooledConnection) |Microsoft 文件
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
ms.topic: article
apiname:
- SQLServerPooledConnection.getConnection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 05bdb61f-26e8-480f-a1c1-1e46a8ed4b70
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1dca9d2d0f97d01cb3f8a4400b4013c3a701372
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="getconnection-method-sqlserverpooledconnection"></a>getConnection 方法 (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立實體連接的物件控制代碼，這[SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)物件表示。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Connection getConnection()  
```  
  
## <a name="return-value"></a>傳回值  
 連接物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 GetConnection 方法，這是由 javax.sql.PooledConnection 介面中的 getConnection 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成員](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 類別](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
