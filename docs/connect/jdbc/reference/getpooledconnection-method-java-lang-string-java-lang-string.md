---
title: getPooledConnection 方法 (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnectionPoolDataSource.getPooledConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f2e6391d-9aaf-4b09-ae1c-a27c1ada6301
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69a9db6da093341264953e698cdbb1145093d9a5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980877"
---
# <a name="getpooledconnection-method-javalangstring-javalangstring"></a>getPooledConnection 方法 (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  嘗試建立可用來當做共用連接的實體資料庫連接 (根據給定的使用者名稱和密碼)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.sql.PooledConnection getPooledConnection(java.lang.String user,  
                                                      java.lang.String password)  
```  
  
#### <a name="parameters"></a>參數  
 *user*  
  
 包含使用者名稱的**字串**。  
  
 *passwword*  
  
 包含密碼的**字串**。  
  
## <a name="return-value"></a>傳回值  
 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getPooledConnection 方法是由 javax.sql.ConnectionPoolDataSource 介面中的 getPooledConnection 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)   
 [SQLServerConnectionPoolDataSource 方法](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-methods.md)   
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [SQLServerConnectionPoolDataSource 類別](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
