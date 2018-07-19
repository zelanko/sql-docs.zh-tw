---
title: getResultSetType 方法 (SQLServerStatement) |Microsoft 文件
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
- SQLServerStatement.getResultSetType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 260da35f-ddf6-4111-8519-69956ea3072e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f03b13c280a53ac52efe1247ff00400b03323f28
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836866"
---
# <a name="getresultsettype-method-sqlserverstatement"></a>getResultSetType 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取結果集類型為[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)這由所產生的物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getResultSetType()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出結果集類型。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getResultSetType 方法是由 java.sql.Statement 介面中的 getResultSetType 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
