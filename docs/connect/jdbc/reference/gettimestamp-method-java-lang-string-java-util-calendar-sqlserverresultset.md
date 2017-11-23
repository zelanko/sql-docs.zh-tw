---
title: "getTimestamp 方法 （java.lang.String，java.util.Calendar） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.getTimestamp (java.lang.String, java.util.Calendar)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 44474000-8951-49ee-93a5-c8cb879eaf55
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 62466b3b77d2ce85fcc9573804b1cd8b7347280e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar-sqlserverresultset"></a>getTimestamp 方法 （java.lang.String，java.util.Calendar） (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行名稱的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)來當做 java.sql.Timestamp 物件在 Java 程式語言，並使用行事曆物件中的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String colName,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>參數  
 *colName*  
  
 A**字串**，其中包含資料行名稱。  
  
 *cal*  
  
 行事曆物件。  
  
## <a name="return-value"></a>傳回值  
 時間戳記的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetTimestamp 方法 java.sql.ResultSet 介面中所指定此 getTimestamp 方法。  
  
 這個方法會傳回值，只能從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]datetime 和 smalldatetime 資料行。  
  
## <a name="see-also"></a>請參閱＜  
 [getTimestamp 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
