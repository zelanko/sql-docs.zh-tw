---
title: "setObject 方法 (SQLServerCallableStatement) |Microsoft 文件"
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
- SQLServerCallableStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b1b11d4929f14543c6930021284c55e9bfbffd6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="setobject-method-sqlservercallablestatement"></a>setObject 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用給定物件，設定指定之參數的值。  
  
 開頭為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0 中，這個方法的行為由修改**sendTimeAsDatetime**連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊，請參閱[如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>多載清單  
  
|名稱|Description|  
|----------|-----------------|  
|[setObject （java.lang.String，java.lang.Object）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|使用給定物件，設定指定之參數的值。|  
|[setObject （java.lang.String，java.lang.Object，int）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|使用給定的物件和目標型別，設定指定之參數的值。|  
|[setObject （java.lang.String，java.lang.Object，int，int）](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|使用給定的物件、目標型別和小數位數，設定指定之參數的值。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 類別](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
