---
title: "addBatch 方法 (java.lang.String) |Microsoft 文件"
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
- SQLServerPreparedStatement.addBatch (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 093f6c3b-49a6-4043-9993-bd0482de04dd
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8febab83df94f0d1f6034c133cdd7e5a95db51ad
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="addbatch-method-javalangstring"></a>addBatch 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將給定的 SQL 命令加入至目前命令清單中，這個[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void addBatch(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**，其中包含 SQL 陳述式。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 addBatch 方法是由 java.sql.Statement 介面中的 addBatch 方法指定。  
  
 呼叫這個方法會導致例外狀況，因為在建立物件時指定 SQLServerPreparedStatement 物件的 SQL 陳述式。  
  
## <a name="see-also"></a>另請參閱  
 [addBatch 方法 &#40;SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

