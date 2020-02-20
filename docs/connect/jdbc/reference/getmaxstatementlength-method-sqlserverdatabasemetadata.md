---
title: getMaxStatementLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxStatementLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f45fcf45-b9e7-4d14-a90a-ebc542ac7755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 205b939a870ede1a5a4a02fec81d73ea8dba073d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67981981"
---
# <a name="getmaxstatementlength-method-sqlserverdatabasemetadata"></a>getMaxStatementLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在 SQL 陳述式中使用的最大字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxStatementLength()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxStatementLength 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxStatementLength 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
