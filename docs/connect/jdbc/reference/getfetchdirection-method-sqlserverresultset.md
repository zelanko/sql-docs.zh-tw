---
title: getFetchDirection 方法 (SQLServerResultSet) |Microsoft 文件
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
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594d59adc33decf67118fd680d6aeaa32a38ebe7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個提取方向[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出目前的提取方向。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetFetchDirection 方法 java.sql.ResultSet 介面中所指定此 getFetchDirection 方法。  
  
 這個方法會傳回 FETCH_FORWARD 順向資料指標，最後呼叫所做的設定[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)方法的其他資料指標類型，則會傳回 FETCH_UNKNOWN 這些資料指標類型和 setFetchDirection 方法永遠不會呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
