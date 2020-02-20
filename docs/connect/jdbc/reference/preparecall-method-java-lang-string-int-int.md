---
title: prepareCall 方法 (java.lang.String, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 04d36a25-7f95-4675-9690-4462671b3d67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7b51cbe470169459469959448208b3aa53b18cce
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976251"
---
# <a name="preparecall-method-javalangstring-int-int"></a>prepareCall 方法 (java.lang.String, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  建立 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件，它會產生具有指定類型和並行的 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int resultSetType,  
                                              int resultSetConcurrency)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 **String**，其中包含 SQL 陳述式。  
  
 *resultSetType*  
  
 **int**，指出結果集類型。  
  
 *resultSetConcurrency*  
  
 **int**，指出結果集的並行類型。  
  
## <a name="return-value"></a>傳回值  
 CallableStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 prepareCall 方法是由 java.sql.Connection 介面中的 prepareCall 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [prepareCall 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
