---
title: isAfterLast 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233599694c4fb4f7764bbb48d5c77e0fcd273340
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977844"
---
# <a name="isafterlast-method-sqlserverresultset"></a>isAfterLast 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出資料指標是否出現在這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的最後一個資料列後面。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>傳回值  
 如果資料指標位於最後一個資料列之後，則為 **true**。 如果資料指標位於其他任何位置或者結果集未包含任何資料列，則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 isAfterLast 方法是由 java.sql.ResultSet 介面中的 isAfterLast 方法指定。  
  
 如果搭配動態資料指標使用這個方法，包括順向的唯讀資料指標，而且 selectMethod 連接屬性設定為 "cursor"，則會發生例外狀況。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
