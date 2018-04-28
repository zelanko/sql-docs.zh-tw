---
title: prepareCall 方法 （java.lang.String，int，int） |Microsoft 文件
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
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0ed9e69d1f7eb914bf26e7da859dc691f8009807
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall 方法 (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件，可產生[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)具有給定型的別和並行存取的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**包含 SQL 陳述式。  
  
 *resultSetType*  
  
 **Int** ，指出結果集類型。  
  
 *resultSetConcurrency*  
  
 **Int** ，指出結果集並行類型。  
  
## <a name="return-value"></a>傳回值  
 CallableStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 prepareCall 方法是由 java.sql.Connection 介面中的 prepareCall 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [prepareCall 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
