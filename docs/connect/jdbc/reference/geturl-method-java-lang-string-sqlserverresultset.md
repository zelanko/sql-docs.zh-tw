---
title: getURL 方法 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getURL (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 105a5319-0f4c-4d08-964b-cc52f8e28ec1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 49f586249657b2f10a166c975608fd2b539d67ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740866"
---
# <a name="geturl-method-javalangstring-sqlserverresultset"></a>getURL 方法 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  從這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件目前資料列中擷取所指定資料行名稱的值來作為 URL 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.net.URL getURL(java.lang.String sColumn)  
```  
  
#### <a name="parameters"></a>參數  
 *sColumn*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 URL 的物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 getURL 方法是由 java.sql.ResultSet 介面中的 getURL 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getURL 方法&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
