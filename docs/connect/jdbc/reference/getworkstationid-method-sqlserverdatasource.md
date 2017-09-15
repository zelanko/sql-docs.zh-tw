---
title: "getWorkstationID 方法 (SQLServerDataSource) |Microsoft 文件"
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
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 452651fee5e24a20da7dc880298d7fb6492d49d6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="getworkstationid-method-sqlserverdatasource"></a>getWorkstationID 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用來連接到資料來源之用戶端電腦的名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含用戶端電腦名稱。  
  
## <a name="remarks"></a>備註  
 workstationID 是用戶端電腦或工作站的名稱。 如果未設定 workstationID 屬性，預設值是藉由呼叫 InetAddress.getLocalHost().getHostName() 方法建構。 如果 getHostName 傳回空白值時，會呼叫 getHostAddress().toString() 方法。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
