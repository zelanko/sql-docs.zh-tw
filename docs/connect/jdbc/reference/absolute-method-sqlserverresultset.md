---
title: absolute 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 298e169fe2b67b16b55d607f504446c48893fc1b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616936"
---
# <a name="absolute-method-sqlserverresultset"></a>absolute 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將資料指標移至這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中的指定資料列。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>參數  
 *row*  
  
 **int**，指出要移至的資料列編號。 可以為正數、負數或 0。  
  
## <a name="return-value"></a>傳回值  
 **true**如果將游標移至指定的位置。 **false**如果它是第一個資料列之前或之後的最後一個資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個絕對的方法是由 java.sql.ResultSet 介面中的絕對方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
