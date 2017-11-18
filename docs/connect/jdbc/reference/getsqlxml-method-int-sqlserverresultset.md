---
title: "getSQLXML 方法 (int) (SQLServerResultSet) |Microsoft 文件"
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
ms.assetid: faa35676-573d-48d5-afd9-850134735728
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f62050319394f50f0fb8e570a57f17389d2dfd0f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlxml-method-int-sqlserverresultset"></a>getSQLXML 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列內指定之資料行的值[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)當做 SQLXML 物件的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.SQLXML getSQLXML(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSQLXML 方法是由 java.sql.ResultSet 介面中的 getSQLXML 方法來指定。  
  
## <a name="see-also"></a>另請參閱  
 [getSQLXML 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  

