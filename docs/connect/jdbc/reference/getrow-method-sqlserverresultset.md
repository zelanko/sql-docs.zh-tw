---
title: getRow 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a266e3bc-05c2-44e2-9346-125ae6780216
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 784ae37816977e08bb52290249d4ee47526cc527
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782766"
---
# <a name="getrow-method-sqlserverresultset"></a>getRow 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前資料列數值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getRow()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出目前的資料列數值，如果沒有任何資料列，則為 0。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getRow 方法是由 java.sql.ResultSet 介面中的 getRow 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
