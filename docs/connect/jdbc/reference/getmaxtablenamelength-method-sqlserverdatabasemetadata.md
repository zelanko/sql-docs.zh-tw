---
title: getMaxTableNameLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxTableNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5c51218f-c6e8-49f4-ad09-292e849ca43a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aebb22867f2efb3b31d235f1df9ae73c85bab5e8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981965"
---
# <a name="getmaxtablenamelength-method-sqlserverdatabasemetadata"></a>getMaxTableNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在資料表名稱中使用的最大字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxTableNameLength()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxTableNameLength 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxTableNameLength 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
