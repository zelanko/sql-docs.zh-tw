---
title: getArray 方法 (int) (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getArray (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 377746c7-8c9c-41f5-8490-ca0dd56fd57a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f993406e24265689f852e1e70515ca24eda6d536
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850506"
---
# <a name="getarray-method-int-sqlserverresultset"></a>getArray 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行索引的值來作為 Array 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Array getArray(int i)  
```  
  
#### <a name="parameters"></a>參數  
 *i*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 陣列物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getArray 方法是由 java.sql.ResultSet 介面中的 getArray 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getArray 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
