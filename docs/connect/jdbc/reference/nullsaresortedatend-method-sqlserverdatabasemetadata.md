---
title: nullsAreSortedAtEnd 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedAtEnd
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 713cf636-40f2-474a-8a5d-5aba4a310a9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 871f7896f0f0053e8b45bd93dedd5153a58b8b25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673276"
---
# <a name="nullsaresortedatend-method-sqlserverdatabasemetadata"></a>nullsAreSortedAtEnd 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出是否一定將 NULL 值排在結尾，無論其排序順序為何。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean nullsAreSortedAtEnd()  
```  
  
## <a name="return-value"></a>傳回值  
 如果排在結尾，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 nullsAreSortedAtEnd 方法是由 java.sql.DatabaseMetaData 介面中 nullsAreSortedAtEnd 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
