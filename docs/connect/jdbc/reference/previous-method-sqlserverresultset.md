---
title: previous 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.previous
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66eb4e10-c375-4b31-ac46-3ba1d9dbf6a0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 587398c10e693081a9dc6a6c4abb61ff970b2f03
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692316"
---
# <a name="previous-method-sqlserverresultset"></a>previous 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將資料指標移動到這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的前一個資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean previous()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**新的目前資料列是否有效。 **false**如果沒有要處理多個資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個先前的方法是由 java.sql.ResultSet 介面中的前一個方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
