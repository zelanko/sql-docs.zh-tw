---
title: getMaxRows 方法 (SQLServerStatement) |Microsoft 文件
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
- SQLServerStatement.getMaxRows
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6aece4e5-027d-434e-a8cf-a67c0484f189
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3af453b1e82984e06da41a03b289107d72d0ce88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="getmaxrows-method-sqlserverstatement"></a>getMaxRows 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取資料列數目上限， [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)產生由此物件[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件可以包含。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getMaxRows()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出資料列或 0 的最大數目，如果沒有任何限制。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxRows 方法是由 java.sql.Statement 介面中的 getMaxRows 方法指定。  
  
 這個 getMaxRows 方法一律會傳回 0 代表動態的可捲動資料指標。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
