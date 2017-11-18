---
title: "createStatement 方法 （int，int，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.createStatement (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2e4fa385-8f61-4394-8f75-3e839930a57d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0298571db91e5f733de531f1ff30de88c457b5f7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="createstatement-method-int-int-int"></a>createStatement 方法 (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件，可產生[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件與指定的型別、 並行和保留性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Statement createStatement(int nType,  
                                          int nConcur,  
                                          int nHold)  
```  
  
#### <a name="parameters"></a>參數  
 *resultSetType*  
  
 **Int**值，表示結果集類型。  
  
 *nConcur*  
  
 **Int**值，表示結果集並行類型。  
  
 *nHold*  
  
 **Int**值，表示保留性。  
  
## <a name="return-value"></a>傳回值  
 陳述式物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 createStatement 方法是由 java.sql.Connection 介面中的 createStatement 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [createStatement 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

