---
title: "executeUpdate 方法 （java.lang.String，int） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb27e4538eccf87257d16555505442f76461adb0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行給定的 SQL 陳述式並訊號[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]有關是否自動產生金鑰的指定旗標所產生的這[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件應該可供擷取。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>參數  
 *sql*  
  
 A**字串**，其中包含 SQL 陳述式。  
  
 *旗標*  
  
 **Int**值，指出是否自動產生的索引鍵可供使用。 這個值一定是下面其中一個常數：  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>傳回值  
 **Int** ，指出資料列受到影響或 0 的數目，如果使用 DDL 陳述式。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 executeUpdate 方法是由 java.sql.Statement 介面中的 executeUpdate 方法指定。  
  
 如果執行預存程序會導致更新計數大於一，或是產生多個結果集，使用[執行](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)方法才能執行預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [executeUpdate 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
