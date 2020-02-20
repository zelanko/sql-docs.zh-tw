---
title: getSQLXML 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f56b192a-3255-4215-b552-8e494fbca083
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 125584fd3ad858a4242f6d85e755b3ec04e50ab1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979638"
---
# <a name="getsqlxml-method-javalangstring"></a>getSQLXML 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  透過指定的參數名稱，擷取所指定參數的值來作為 SQLXML 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>參數  
 *parameterName*  
  
 指出參數名稱的**字串**。  
  
## <a name="return-value"></a>傳回值  
 ASQLXMLobject。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getSQLXML 方法是由 java.sql.CallableStatement 介面中的 getSQLXML 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [getSQLXML 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成員](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
