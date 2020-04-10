---
title: getAsciiStream 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getAsciiStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2d24a6b-f029-4691-981b-125c690b8ba5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55709acd48aec185d06a09acd48951424cf8cc90
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925422"
---
# <a name="getasciistream-method-javalangstring"></a>getAsciiStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件中目前資料列內指定之資料行名稱的值來當作 ASCII 字元資料流。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.InputStream getAsciiStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>參數  
 *columnName*  
  
 包含資料行名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 InputStream 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getAsciiStream 方法是由 java.sql.ResultSet 介面中的 getAsciiStream 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [getAsciiStream 方法 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
