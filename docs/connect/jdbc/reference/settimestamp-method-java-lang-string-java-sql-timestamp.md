---
title: "setTimestamp 方法時間戳記值 |Microsoft 文件"
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
apiname: SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: dc45b126-3196-47ff-956b-cbc897980ff8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96d2cac5175dbe4dfc63e96afd1cb8676e750dff
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp"></a>setTimestamp 方法 (java.lang.String, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間戳記值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp t)  
```  
  
#### <a name="parameters"></a>參數  
 *sCol*  
  
 A**字串**，其中包含參數名稱。  
  
 *t*  
  
 時間戳記的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetTimestamp 方法 java.sql.CallableStatement 介面中所指定此 setTimestamp 方法。  
  
## <a name="see-also"></a>請參閱＜  
 [setTimestamp 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
