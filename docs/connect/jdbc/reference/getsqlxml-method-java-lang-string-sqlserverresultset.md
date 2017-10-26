---
title: "getSQLXML 方法 (java.lang.String) (SQLServerResultSet) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9c7b10-026f-4a51-8d60-e6871d1abd02
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62f5ddac783abb349b9338f954fbefc5c31a7126
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlxml-method-javalangstring-sqlserverresultset"></a>getSQLXML 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列內指定之資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 SQLXML 物件的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 A**字串**，指出資料行標籤。  
  
## <a name="return-value"></a>傳回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSQLXML 方法是由 java.sql.ResultSet 介面中的 getSQLXML 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [getSQLXML 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  

