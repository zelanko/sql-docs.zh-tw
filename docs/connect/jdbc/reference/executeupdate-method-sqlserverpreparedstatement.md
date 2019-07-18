---
title: executeUpdate 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 677b0907-316e-40f2-a0d9-d4d0872c7f52
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: db7d44384e097888d0ab63fdd27d2228ecd37bda
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804142"
---
# <a name="executeupdate-method-sqlserverpreparedstatement"></a>executeUpdate 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  在這個 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件中執行的 SQL 陳述式必須是 SQL INSERT、UPDATE、MERGE 或 DELETE 陳述式；否則這個陳述式必須是不傳回任何項目的 SQL 陳述式，例如 DDL 陳述式。  
  
## <a name="overload-list"></a>多載清單  
  
|[屬性]|Description|  
|----------|-----------------|  
|[executeUpdate ()](../../../connect/jdbc/reference/executeupdate-method.md)|在這個 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件中執行的 SQL 陳述式必須是 SQL INSERT、UPDATE、MERGE 或 DELETE 陳述式；否則這個陳述式必須是不傳回任何項目的 SQL 陳述式，例如 DDL 陳述式。|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|執行可能是 INSERT、UPDATE、MERGE 或 DELETE 陳述式的給定 SQL 陳述式，否則會是不傳回任何項目的 SQL 陳述式，例如 SQL DDL 陳述式。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
