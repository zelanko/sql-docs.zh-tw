---
title: getResultSet 方法 (SQLServerStatement) |Microsoft 文件
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
- SQLServerStatement.getResultSet
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 929a14e2-8e98-4c32-89aa-86733c717ec1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cfa88e7501f9781507b72132cc4b7fa703726cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836886"
---
# <a name="getresultset-method-sqlserverstatement"></a>getResultSet 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前結果當做[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.ResultSet getResultSet()  
```  
  
## <a name="return-value"></a>傳回值  
 結果集物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getResultSet 方法是由 java.sql.Statement 介面中 getResultSet 方法，可指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
