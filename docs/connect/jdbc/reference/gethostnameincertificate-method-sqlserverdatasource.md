---
title: getHostNameInCertificate 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 67978d2597a5167d3930c85ee453dc6d985f021e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982906"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>getHostNameInCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回用於驗證 SQL Server 安全通訊端層 (SSL) 憑證的主機名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>傳回值  
 包含主機名稱的 **String**，如果未設定任何值，則為 null。  
  
## <a name="remarks"></a>Remarks  
 使用 SSL 加密通訊層時，便會使用主機名稱來驗證 SQL Server SSL 憑證值。  
  
 如果未設定主機名稱，[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) 方法會傳回 null。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
