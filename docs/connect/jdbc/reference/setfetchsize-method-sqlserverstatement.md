---
title: "setFetchSize 方法 (SQLServerStatement) |Microsoft 文件"
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
apiname: SQLServerStatement.setFetchSize
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69aaab5db90e9affaa46f1bb9aff80265f9759e4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setfetchsize-method-sqlserverstatement"></a>setFetchSize 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  提供[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提示，當做在需要更多的資料列時應該從資料庫提取的資料列數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>參數  
 *資料列*  
  
 **Int** ，指出要提取的資料列數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setFetchSize 方法是由 java.sql.Statement 介面中的 setFetchSize 方法指定。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
