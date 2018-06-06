---
title: getTimestamp 方法 (int) (SQLServerResultSet) |Microsoft 文件
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
- SQLServerResultSet.getTimestamp (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ad538a76-983f-4175-9481-9e7fa9480c71
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3511b1226d63df4ea4bf9b7a947dc861e54bfcfb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="gettimestamp-method-int-sqlserverresultset"></a>getTimestamp 方法 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行索引的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)來當做 java.sql.Timestamp 物件在 Java 程式語言中的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Timestamp getTimestamp(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
## <a name="return-value"></a>傳回值  
 時間戳記的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetTimestamp 方法 java.sql.ResultSet 介面中所指定此 getTimestamp 方法。  
  
 這個方法會傳回值，只能從[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]datetime 和 smalldatetime 資料行。  
  
## <a name="see-also"></a>另請參閱  
 [getTimestamp 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
