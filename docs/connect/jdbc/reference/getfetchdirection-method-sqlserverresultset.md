---
title: getFetchDirection 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: efd432f446efaef2c8d3d391c98ea1ba72a3f662
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803040"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的擷取方向。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出目前的提取方向。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getFetchDirection 方法是由 java.sql.ResultSet 介面中的 getFetchDirection 方法指定。  
  
 這個方法會針對順向的資料指標傳回 FETCH_FORWARD，這是呼叫其他資料指標類型 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) 方法所做的最後一項設定，而且如果從未呼叫 setFetchDirection 方法，將會針對這些資料指標類型傳回 FETCH_UNKNOWN。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
