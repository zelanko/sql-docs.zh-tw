---
title: "getClientInfo 方法 (java.lang.String) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e0f92e5db61ef0b778e293ea61b25ad61956986a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之用戶端資訊屬性的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>參數  
 *name*  
  
 字串，包含要擷取之用戶端資訊屬性的名稱。  
  
## <a name="return-value"></a>傳回值  
 字串，包含用戶端資訊屬性的值。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetClientInfo 方法 java.sql.Connection 介面中所指定此 getClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支援任何用戶端資訊屬性。 如此一來，這個方法會傳回**null**。  
  
 同樣地，應用程式可以使用[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)類別來擷取此驅動程式支援之用戶端資訊屬性的清單。 [GetClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法會傳回空的結果集。  
  
## <a name="see-also"></a>另請參閱  
 [getClientInfo 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

