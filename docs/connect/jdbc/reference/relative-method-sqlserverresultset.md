---
title: relative 方法 (SQLServerResultSet) | Microsoft Docs
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
ms.openlocfilehash: 5b2e644feff3cd2787cc6bd80bce54562ad20794
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975779"
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
 這個相對方法是由 sql ResultSet 介面中的相對方法指定。  
  
 嘗試移到結果集中第一個或最後一個資料列之外的範圍會將游標置於第一個或最後一個資料列之前或之後。 呼叫 `relative(0)` 是有效的，但不會變更游標位置。  
  
 呼叫 `relative(1)` 方法等於呼叫 [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) 方法。 呼叫 `relative(-1)` 方法等於呼叫 [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
