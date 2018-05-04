---
title: executeUpdate 方法 (java.lang.String) (SQLServerStatement) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85e7c3a2-f2da-49bf-9d90-5fd246fd60e1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 148f2887e01d5238ac7461f4922eea77af599bdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="executeupdate-method-javalangstring-sqlserverstatement"></a>executeUpdate 方法 (java.lang.String) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行可能是 INSERT、UPDATE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。 從開始[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 中，executeUpdate 將會傳回正確的更新合併作業中的資料列數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int executeUpdate(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**，其中包含 SQL 陳述式。  
  
## <a name="return-value"></a>傳回值  
 **int** 會指出受影響的資料列數目，如果是使用 DDL 陳述式，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 executeUpdate 方法是由 java.sql.Statement 介面中的 executeUpdate 方法指定。  
  
 如果執行預存程序產生的更新計數大於一或是產生一個以上的結果集，請使用 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 方法執行預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
