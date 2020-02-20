---
title: getClob 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1de9804-1f27-4854-8985-3385fadcbebb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e0eee2cafe95e04ffd5c697667cac2701ee0b80
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953036"
---
# <a name="getclob-method-javalangstring-sqlserverresultset"></a>getClob 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 Java 程式設計語言，從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行名稱的值來作為 Clob 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.sql.Clob getClob(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>參數  
 *colName*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 Clob 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getClob 方法是由 java.sql.ResultSet 介面中的 getClob 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
