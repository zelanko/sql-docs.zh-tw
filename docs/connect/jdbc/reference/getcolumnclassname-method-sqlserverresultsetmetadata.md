---
title: getColumnClassName 方法 (SQLServerResultSetMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2c118790-5dd2-4b10-93b6-7f065ee324ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8e76d8dc4944440eeae5017f6e383af27ad4103
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680319"
---
# <a name="getcolumnclassname-method-sqlserverresultsetmetadata"></a>getColumnClassName 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 Java 類別的完整名稱，此類別執行個體會在呼叫 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 類別的 [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) 方法來從資料行擷取值時進行製造。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getColumnClassName(int column)  
```  
  
#### <a name="parameters"></a>參數  
 *column*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 **String**，其中包含類別的完整名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getColumnClassName 方法是由 java.sql.ResultSetMetaData 介面中 getColumnClassName 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成員](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 類別](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
