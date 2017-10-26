---
title: "getClientInfo 方法 （) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b06a5ced-b760-4c78-b17e-854ce95a1a5c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed81345b9cf45678fd4571fca747eebb7fc30f9b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getclientinfo-method-"></a>getClientInfo 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取清單，此清單包含 JDBC Driver 所支援之個別用戶端資訊的名稱和最新值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.util.Properties getClientInfo()  
```  
  
## <a name="return-value"></a>傳回值  
 包含名稱和每個驅動程式支援的用戶端資訊屬性的目前值的屬性物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetClientInfo 方法 java.sql.Connection 介面中所指定此 getClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支援任何用戶端資訊屬性。 如此一來，這個方法會傳回空的屬性物件。  
  
 同樣地，應用程式可以使用[getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)類別來擷取此驅動程式支援之用戶端資訊屬性的清單。 [GetClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md)方法會傳回空的結果集。  
  
## <a name="see-also"></a>另請參閱  
 [getClientInfo 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

