---
title: "setTimestamp 方法 （int，java.sql.Timestamp） |Microsoft 文件"
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
apiname: SQLServerPreparedStatement.setTimestamp (int, java.sql.Timestamp)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 2f7bb89f-ace7-41cb-b596-5aa8d0dd9e3c
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: abbc7756ab0b62f12210b6bcf44040730b42ab3a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="settimestamp-method-int-javasqltimestamp"></a>setTimestamp 方法 (int, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將指定的參數設定為給定的時間戳記值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setTimestamp(int n,  
                               java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **Int** ，指出參數編號。  
  
 *x*  
  
 時間戳記的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetTimestamp 方法 java.sql.PreparedStatement 介面中所指定此 setTimestamp 方法。  
  
## <a name="see-also"></a>請參閱＜  
 [setTimestamp 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
