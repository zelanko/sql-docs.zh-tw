---
title: setObject 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 93a2b22c-82b4-48c7-a428-369ebe98a372
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eba5beb14bc30fb8e8935bd07a12971a25e5cce6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788052"
---
# <a name="setobject-method-sqlserverpreparedstatement"></a>setObject 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用給定物件，設定指定之參數的值。  
  
 開頭[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]JDBC 驅動程式 3.0 中，這個方法的行為由修改**sendTimeAsDatetime**連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="overload-list"></a>多載清單  
  
|[屬性]|Description|  
|----------|-----------------|  
|[setObject (int, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object.md)|使用給定物件，設定指定之參數的值。|  
|[setObject (int, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int.md)|使用給定的物件和目標型別，設定指定之參數的值。|  
|[setObject (int, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-int-java-lang-object-int-int.md)|使用給定的物件、目標型別和小數位數，設定指定之參數的值。|  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
