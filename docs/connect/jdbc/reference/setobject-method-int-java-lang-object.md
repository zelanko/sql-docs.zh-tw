---
title: setObject 方法 (int, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setObject (int, java.lang.Object)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 61f19faa-3006-4a1c-974c-55951e3b3000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e4ab210a30080472a777d151695a04ec49ff1041
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973377"
---
# <a name="setobject-method-int-javalangobject"></a>setObject 方法 (int, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用給定物件，設定指定之參數的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setObject(int index,  
                            java.lang.Object obj)  
```  
  
#### <a name="parameters"></a>參數  
 *index*  
  
 **int**，指出參數編號。  
  
 *obj*  
  
 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setObject 方法由 java.sql.PreparedStatement 介面中的 setObject 方法指定。  
  
 在呼叫這個 setObject 方法前，應用程式可以使用下列其中一個方法來設定指定的參數：  
  
-   SQLServerPreparedStatement 類別或 SQLServerCallableStatement 類別的 set\<Type> 方法  
  
-   SQLServerPreparedStatement 類別或 SQLServerCallableStatement 類別的 setNull 方法  
  
-   SQLServerCallableStatement 類別的[registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)方法  
  
 在這種情況下，將會自動設定參數的型別。 如果應用程式搭配 obj 值 NULL 呼叫這個 setObject 方法，驅動程式會假設參數類型為先前呼叫方法所設定的類型。  
  
 如果 obj 值為 NULL 而且無法判斷該參數的類型資訊，setObject 方法會將指定的參數轉換成 CHAR，然後將其傳送給資料庫。  
  
 從 JDBC Driver 3.0 開始, **sendTimeAsDatetime** 連接屬性會修改這個方法的行為 ([設定連接屬性](../../../connect/jdbc/setting-the-connection-properties.md)) 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [SQLServerDataSource. Sqlserverdatasource.setsendtimeasdatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。  
  
 如需詳細資訊, 請參閱設定將[java. Time 值傳送至伺服器的方式](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [setObject 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
