---
title: "getBoolean 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getBoolean (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ba98a27b-722d-4904-ac65-0f082fde1fe6
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72721ed397e2c88042ad30bdd414f43645a0889a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getboolean-method-javalangstring-sqlserverresultset"></a>getBoolean 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行名稱的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做**布林**在 Java 程式語言。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getBoolean(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 A**字串**，其中包含資料行名稱。  
  
## <a name="return-value"></a>傳回值  
 A**布林**值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBoolean 方法 java.sql.ResultSet 介面中所指定此 getBoolean 方法。  
  
 只有在數字和字元資料類型上才支援這個方法。 它會將值"1"，1，為和"**true**"來**，則為 true**，和值"0"，0，和"**false**"至**false**。 如果是所有其他值，則不會定義這個行為。  
  
## <a name="see-also"></a>另請參閱  
 [getBoolean 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

