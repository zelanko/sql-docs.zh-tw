---
title: getFetchDirection 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ab385c2-e18c-4b75-ac2d-2402af5c52a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73a507e48b4ecc7f1ead7e33fe6936f5ed73f424
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924832"
---
# <a name="getfetchdirection-method-sqlserverresultset"></a>getFetchDirection 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的擷取方向。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getFetchDirection()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出目前的提取方向。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getFetchDirection 方法是由 java.sql.ResultSet 介面中的 getFetchDirection 方法指定。  
  
 這個方法會針對順向的資料指標傳回 FETCH_FORWARD，這是呼叫其他資料指標類型 [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md) 方法所做的最後一項設定，而且如果從未呼叫 setFetchDirection 方法，將會針對這些資料指標類型傳回 FETCH_UNKNOWN。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
