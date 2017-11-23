---
title: "setTimestamp 方法時間戳記和行事曆值 |Microsoft 文件"
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
apiname: SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp, java.util.Calendar))
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 09dca1f9-225a-4acb-9857-9a947e0829be
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f8a03050ce13735ea1e4adaf35fec1563885b9ff
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp-javautilcalendar"></a>setTimestamp 方法 (java.lang.String, java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間戳記和行事曆值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp x,  
                         java.util.Calendar c)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
 *x*  
  
 時間戳記的物件。  
  
 *c*  
  
 行事曆物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetTimestamp 方法 java.sql.CallableStatement 介面中所指定此 setTimestamp 方法。  
  
## <a name="see-also"></a>請參閱＜  
 [setTimestamp 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
