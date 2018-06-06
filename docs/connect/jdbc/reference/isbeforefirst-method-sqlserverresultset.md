---
title: isBeforeFirst 方法 (SQLServerResultSet) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1df75b7fd5e0728275b5a431855ffdc3db3d8a10
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="isbeforefirst-method-sqlserverresultset"></a>isBeforeFirst 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值之前的第一個資料列在這個游標是否[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果游標位於第一個資料列之前。 **false**如果資料指標位於其他任何位置或者結果集包含任何資料列。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isBeforeFirst 方法是由 java.sql.ResultSet 介面中的 isBeforeFirst 方法指定。  
  
 如果搭配動態資料指標使用這個方法，包括順向的唯讀資料指標，而且 selectMethod 連接屬性設定為 "cursor"，則會發生例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
