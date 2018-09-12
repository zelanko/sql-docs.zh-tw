---
title: executeUpdate 方法 (SQLServerStatement) |Microsoft Docs
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
- SQLServerStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1118d231c1eb60f70c9944cd6ede5991d05b5d2c
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785260"
---
# <a name="executeupdate-method-sqlserverstatement"></a>executeUpdate 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  執行可能是 INSERT、UPDATE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。 從 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 開始，executeUpdate 將會傳回 MERGE 作業中更新的正確資料列數目。  
  
## <a name="overload-list"></a>多載清單  
  
|[屬性]|Description|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|執行可能是 INSERT、UPDATE、DELETE 或 MERGE 陳述式的給定 SQL 陳述式，否則會是不傳回任何內容的 SQL 陳述式，例如 SQL DDL 陳述式。|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|執行指定的 SQL 陳述式，並透過指定的旗標向 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 發出訊號，通知是否要提供由這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件產生的自動產生索引鍵來進行擷取。|  
|[executeUpdate (java.lang.String, int&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|執行給定的 SQL 陳述式，並向 JDBC Driver 發出信號，通知必須提供在給定陣列中所指出的自動產生索引鍵以進行擷取。|  
|[executeUpdate (java.lang.String, java.lang.String&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|執行給定的 SQL 陳述式，並向 JDBC Driver 發出信號，通知必須提供在給定陣列中所指出的自動產生索引鍵以進行擷取。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
