---
title: isLast 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85d4451f-6392-470e-ab21-78a495b45792
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9030898e71ec13a75da9b91e41f9792d31cce82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798019"
---
# <a name="islast-method-sqlserverresultset"></a>isLast 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的最後一個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isLast()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果游標位於最後一個資料列。 **false**如果資料指標位於其他任何位置或者結果集包含任何資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 isLast 方法是由 java.sql.ResultSet 介面中的 isLast 方法指定。  
  
 如果搭配順向和動態資料指標使用這個方法，則會擲回例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
