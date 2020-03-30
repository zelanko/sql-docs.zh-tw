---
title: findColumn 方法 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.findColumn
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7c29994a-0b53-420b-8a9b-82a9eef08587
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24aed500f5b345e2ba3762bdd7a888fc5f8f31ba
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954578"
---
# <a name="findcolumn-method-sqlserverresultset"></a>findColumn 方法 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取與這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中所指定資料行名稱相符的第一個資料行索引。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int findColumn(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 **String**，包含資料行的名稱。  
  
## <a name="return-value"></a>傳回值  
 指出資料行索引的 **int**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 findColumn 方法是由 java.sql.ResultSet 介面中的 findColumn 方法指定。  
  
 如果有多個資料行同名，findColumn 方法會傳回第一個區分大小寫的相符項目。 如果沒有任何區分大小寫的相符項目，這個方法會傳回第一個不區分大小寫的相符項目。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
