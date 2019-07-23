---
title: getMetaData 方法 (SQLServerPreparedStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.getMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ed49a53-ed61-4e95-ad67-45957aaabb6a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbc0a0493498f3d216c9e1395f651d8afec70711
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981851"
---
# <a name="getmetadata-method-sqlserverpreparedstatement"></a>getMetaData 方法 (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [SQLServerResultSetMetaData Class](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) 物件，此物件包含當執行這個 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 物件時將傳回 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件資料行的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.ResultSetMetaData getMetaData()  
```  
  
## <a name="return-value"></a>傳回值  
 ResultSetMetaData 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getMetaData 方法是由 JAVA.sql.preparedstatement 介面中的 getMetaData 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPreparedStatement 成員](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 類別](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
