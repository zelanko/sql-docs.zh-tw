---
title: "getBigDecimal 方法 （java.lang.String，int） (SQLServerResultSet) |Microsoft 文件"
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
- SQLServerResultSet.getBigDecimal (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 572a1799-c232-400f-b8d8-37a5719a8d5e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 35c74151c80a626662775f31014f257dc503df1a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getbigdecimal-method-javalangstring-int-sqlserverresultset"></a>getBigDecimal 方法 （java.lang.String，int） (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行名稱的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件使用指定的小數位數。  
  
> [!NOTE]  
>  這個方法在 JDBC 規格中已被取代。 相反地，您應該使用[getBigDecimal (java.lang.String)](../../../connect/jdbc/reference/getbigdecimal-method-java-lang-string-sqlserverresultset.md)方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.math.BigDecimal getBigDecimal(java.lang.String columnName,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 A**字串**，其中包含資料行名稱。  
  
 *scale*  
  
 **Int** ，指出小數點右邊的位數。  
  
## <a name="return-value"></a>傳回值  
 BigDecimal 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetBigDecimal 方法 java.sql.ResultSet 介面中所指定這個 getBigDecimal 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getBigDecimal 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

