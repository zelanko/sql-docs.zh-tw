---
title: setObject 方法 (int, java.lang.Object, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d190ee20-d669-4c6f-a081-d5cfec2f72ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da06abf7222931551ca1ef9b441687837b2c65f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787536"
---
# <a name="setobject-method-int-javalangobject-int-int"></a>setObject 方法 (int, java.lang.Object, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用給定的物件、目標型別和小數位數，設定指定之參數的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setObject(int n,  
                            java.lang.Object obj,  
                            int targetSqlType,  
                            int scale)  
```  
  
#### <a name="parameters"></a>參數  
 *n*  
  
 **int**，指出參數編號。  
  
 *obj*  
  
 物件。  
  
 *targetSqlType*  
  
 **int**，指出 java.sql.Types 中定義的目標類型。  
  
 *scale*  
  
 **int**，指出小數點右邊的位數。 NUMERIC 和 DECIMAL 以外的所有型別都會忽略這個參數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setObject 方法由 java.sql.PreparedStatement 介面中的 setObject 方法指定。  
  
 開頭[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]JDBC 驅動程式 3.0 中，這個方法的行為由修改**sendTimeAsDatetime**連接屬性 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 如何設定 java.sql.Time 值傳送給伺服器](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setObject 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
