---
title: "getTrustServerCertificate 方法 (SQLServerDataSource) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: getTrustServerCertificate Method (SQLServerDataSource)
apilocation: getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fbc992d3ae27a2c519e653d77ec8acbb160d2fe5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回**布林**值，指出是否啟用 trustServerCertificate 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果啟用 trustServerCertificate 則。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 trustServerCertificate 屬性設定為**true**、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Secure Sockets Layer (SSL) 憑證在使用 SSL 加密通訊層時會自動信任。 換句話說，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]將不會驗證[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 憑證。 預設值是 **false**秒。  
  
 如果 trustServerCertificate 屬性設定為**false**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]會驗證伺服器 SSL 憑證。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
