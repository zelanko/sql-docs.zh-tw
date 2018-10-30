---
title: getStatement 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getStatement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dea981b-b4fd-4f8d-954f-e686124627e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 880572925fb1eeb9a9b6f7becbe42d6ed5601d28
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47635196"
---
# <a name="getstatement-method-sqlserverresultset"></a>getStatement 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取產生這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Statement getStatement()  
```  
  
## <a name="return-value"></a>傳回值  
 SQLServerStatement 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getStatement 方法是由 java.sql.ResultSet 介面中的 getStatement 方法指定。  
  
 如果結果集是以其他方式所產生，例如透過 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 方法，這個方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
