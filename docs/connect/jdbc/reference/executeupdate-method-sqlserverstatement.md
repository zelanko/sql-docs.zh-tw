---
title: "executeUpdate 方法 (SQLServerStatement) |Microsoft 文件"
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
apiname: SQLServerStatement.executeUpdate
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8c0c1f5238ece3adb72f108061742034b3df159f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="executeupdate-method-sqlserverstatement"></a>executeUpdate 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行可能是 INSERT、UPDATE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。 從開始[!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 中，executeUpdate 將會傳回正確的更新合併作業中的資料列數目。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|Description|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|執行可能是 INSERT、UPDATE、DELETE 或 MERGE 陳述式的給定 SQL 陳述式，否則會是不傳回任何內容的 SQL 陳述式，例如 SQL DDL 陳述式。|  
|[executeUpdate （java.lang.String，int）](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|執行給定的 SQL 陳述式並訊號[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]與給定的旗標是否自動產生的索引鍵所產生的這[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件應該可供擷取。|  
|[executeUpdate (java.lang.String，int &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|執行給定的 SQL 陳述式，並向 JDBC Driver 發出信號，通知必須提供在給定陣列中所指出的自動產生索引鍵以進行擷取。|  
|[executeUpdate (java.lang.String，java.lang.String &#91; &#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|執行給定的 SQL 陳述式，並向 JDBC Driver 發出信號，通知必須提供在給定陣列中所指出的自動產生索引鍵以進行擷取。|  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
