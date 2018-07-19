---
title: supportsUnion 方法 (SQLServerDatabaseMetaData) |Microsoft 文件
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
- SQLServerDatabaseMetaData.supportsUnion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a757ea51-ff2e-4848-adaf-d9373e418fa3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60f0386584731b8e7d5dab4d2c6593e87aca5b08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32848823"
---
# <a name="supportsunion-method-sqlserverdatabasemetadata"></a>supportsUnion 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援 SQL UNION。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsUnion()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**受支援。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsUnion 方法是由 java.sql.DatabaseMetaData 介面中 supportsUnion 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
