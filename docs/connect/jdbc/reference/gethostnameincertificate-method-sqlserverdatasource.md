---
title: "getHostNameInCertificate 方法 (SQLServerDataSource) |Microsoft 文件"
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
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d74305f9c389da375a26bf0516f577939b50f7e9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>getHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用於驗證 SQL Server 安全通訊端層 (SSL) 憑證的主機名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**，其中包含主機名稱，或如果未不設定任何值則為 null。  
  
## <a name="remarks"></a>備註  
 使用 SSL 加密通訊層時，便會使用主機名稱來驗證 SQL Server SSL 憑證值。  
  
 如果未設定主機名稱， [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

