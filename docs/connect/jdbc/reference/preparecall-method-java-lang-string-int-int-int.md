---
title: "prepareCall 方法 （java.lang.String，int，int，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac3d0d3c239c76d187954e6a4568a140aba73ade
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall 方法 (java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件，可產生[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件與指定的型別、 並行和保留性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
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
 CallableStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 prepareCall 方法是由 java.sql.Connection 介面中的 prepareCall 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [prepareCall 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

