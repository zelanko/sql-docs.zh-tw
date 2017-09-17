---
title: "getCatalog 方法 (SQLServerConnection) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac9650ac08ac3cae7169a2f746d050ccbed7d6f6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalog-method-sqlserverconnection"></a>getCatalog 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前的目錄名稱，這個[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含目錄名稱。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getCatalog 方法是由 java.sql.Connection 介面中的 getCatalog 方法指定。  
  
 如果未設定，則傳回目前目錄屬性的 SQLServerConnection 物件或 null。 目錄屬性會明確設定與[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)方法，或藉由讀取 TDS 上的環境變更為目前目錄以隱含方式更新。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
