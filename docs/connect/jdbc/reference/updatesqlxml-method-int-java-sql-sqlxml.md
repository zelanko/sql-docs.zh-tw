---
title: updateSQLXML 方法 (int, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee90c33b2b546a3eaf48d52b7577200b7c23306b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67998275"
---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>updateSQLXML 方法 (int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  使用 java.sql.SQLXML 值，更新指定的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 指出資料行索引的 **int**。  
  
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
  
  
