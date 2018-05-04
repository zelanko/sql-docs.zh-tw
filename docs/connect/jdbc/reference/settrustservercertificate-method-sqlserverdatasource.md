---
title: setTrustServerCertificate 方法 (SQLServerDataSource) |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb5923c3078944a446abfc763c76122f44af2396
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>setTrustServerCertificate 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定**布林**值，指出是否啟用 trustServerCertificate 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>參數  
 *TrustServerCertificate*  
  
 **true** ，當使用 SSL 加密通訊層時如果伺服器安全通訊端層 (SSL) 憑證應該要自動信任。 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 trustServerCertificate 屬性設定為**true**、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]當使用 SSL 加密通訊層時，會自動信任 SSL 憑證。 換句話說，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]將不會驗證[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]SSL 憑證。 預設值是 **false**秒。  
  
 如果 trustServerCertificate 屬性設定為**false**、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]會驗證伺服器 SSL 憑證。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
