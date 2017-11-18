---
title: "getTrustStore 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e23a59adeb94be0f7cacebdc40fb442c3c69f9ae
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="gettruststore-method-sqlserverdatasource"></a>getTrustStore 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回憑證 trustStore 檔案的路徑 (包括檔案名稱)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>傳回值  
 A**字串**其中包含的路徑 （包括檔案名稱） 的憑證 trustStore 檔案或為 null，如果未不設定任何值。  
  
## <a name="remarks"></a>備註  
 如果未設定 trustStore 屬性， [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

