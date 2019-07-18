---
title: updateSQLXML 方法 (java.lang.String, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f974ec5ac49a22858231526a28dbfb1ab2aa07e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66801685"
---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>updateSQLXML 方法 (java.lang.String, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.SQLXML 值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>參數  
 *columnLabel*  
  
 **String** 指出資料行標籤。  
  
 *xmlObject*  
  
 SQLXML 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 updateSQLXML 方法是由 java.sql.ResultSet 介面中的 updateSQLXML 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [updateSQLXML 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
