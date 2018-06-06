---
title: relative 方法 (SQLServerResultSet) |Microsoft 文件
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
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ede86bd361d4ca496eb4d99cd7b01b1e7a7ee886
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="relative-method-sqlserverresultset"></a>relative 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將游標移動給定資料列數 (相對於目前資料列)，無論是正向或負向。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>參數  
 *nRows*  
  
 **Int** ，指出要移動的資料列數目。  
  
## <a name="return-value"></a>傳回值  
 **true**游標是否位於資料列上。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此相對的方法是由 java.sql.ResultSet 介面中的相對方法所指定。  
  
 嘗試移到結果集中第一個或最後一個資料列之外的範圍會將游標置於第一個或最後一個資料列之前或之後。 呼叫`relative(0)`有效，但不會變更游標位置。  
  
 呼叫方法`relative(1)`等同於呼叫[下一步](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)方法。 呼叫方法`relative(-1)`等同於呼叫[先前](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
