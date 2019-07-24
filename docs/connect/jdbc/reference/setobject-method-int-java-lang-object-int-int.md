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
ms.openlocfilehash: 248b877ecbcda7ce69469fca67ecf3e3a22b54e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973483"
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
  
 從 JDBC Driver 3.0 開始, **sendTimeAsDatetime** 連接屬性會修改這個方法的行為 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊, 請參閱設定將[java. Time 值傳送至伺服器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setObject 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
