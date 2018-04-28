---
title: createStatement 方法 （int，int） |Microsoft 文件
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
- SQLServerConnection.createStatement (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90dbf639-c3d8-4519-9300-5447c79aec17
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35159e03d59aa9b1f4029c4a038555e2ec384895
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="createstatement-method-int-int"></a>createStatement 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件，可產生[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)具有給定型的別和並行存取的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Statement createStatement(int resultSetType,  
                                          int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>參數  
 *resultSetType*  
  
 **Int**值，表示結果集類型。  
  
 *resultSetConcurrency*  
  
 **Int**值，表示結果集並行類型。  
  
## <a name="return-value"></a>傳回值  
 陳述式物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 createStatement 方法是由 java.sql.Connection 介面中的 createStatement 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [createStatement 方法&#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
