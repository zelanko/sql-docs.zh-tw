---
title: relative 方法 (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b8907a5e2eb2ead5202e8aec9fd5320a6047a5f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797711"
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
  
 **int**，指出要移動之資料列的數目。  
  
## <a name="return-value"></a>傳回值  
 如果游標在資料列上，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此相對的方法是由 java.sql.ResultSet 介面中的相對方法所指定。  
  
 嘗試移到結果集中第一個或最後一個資料列之外的範圍會將游標置於第一個或最後一個資料列之前或之後。 呼叫 `relative(0)` 是有效的，但不會變更游標位置。  
  
 呼叫 `relative(1)` 方法等於呼叫 [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) 方法。 呼叫 `relative(-1)` 方法等於呼叫 [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
