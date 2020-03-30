---
title: supportsOrderByUnrelated 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOrderByUnrelated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9ea6c534-8132-49f3-aac3-a12ec4c46df2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5ddbb8fa811a4370db06b4992eb43e26845e1298
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969079"
---
# <a name="supportsorderbyunrelated-method-sqlserverdatabasemetadata"></a>supportsOrderByUnrelated 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援在 ORDER BY 子句中使用未出現在 SELECT 陳述式中的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsOrderByUnrelated()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 此 supportsOrderByUnrelated 方法是由 java.sql.DatabaseMetaData 介面中的 supportsOrderByUnrelated 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
