---
title: "prepareStatement 方法 （java.lang.String，int，int，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3356b173391b2b9aa118f7806fbb6645412bcda2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>prepareStatement 方法 (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)物件，可產生[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件與指定的型別、 並行和保留性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int nType,  
                                                   int nConcur,  
                                                   int nHold)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**包含 SQL 陳述式。  
  
 *n*  
  
 **Int** ，指出結果集類型。  
  
 *nConcur*  
  
 **Int** ，指出結果集並行類型。  
  
 *nHold*  
  
 **Int** ，指出結果集保留性。  
  
## <a name="return-value"></a>傳回值  
 PreparedStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 prepareStatement 方法是由 java.sql.Connection 介面中的 prepareStatement 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [prepareStatement 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
