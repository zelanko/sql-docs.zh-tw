---
title: getAsciiStream 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getAsciiStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2d24a6b-f029-4691-981b-125c690b8ba5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ff964eebb92eb6b4642b2dde7d7f19cdbaf742b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618716"
---
# <a name="getasciistream-method-javalangstring"></a>getAsciiStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列內指定之資料行名稱的值來當作 ASCII 字元資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.InputStream getAsciiStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 GetAsciiStream 方法 java.sql.ResultSet 介面中所指定這個 getAsciiStream 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getAsciiStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
