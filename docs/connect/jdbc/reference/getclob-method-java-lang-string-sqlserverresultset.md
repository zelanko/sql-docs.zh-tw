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
manager: craigg
ms.openlocfilehash: a22148e21a8a4efd451bb7dac2a9a05ea2873229
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806110"
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
  
## <a name="remarks"></a>Remarks  
 GetClob 方法 java.sql.ResultSet 介面中所指定這個 getClob 方法。  
  
## <a name="see-also"></a>另請參閱  
 [getClob 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
