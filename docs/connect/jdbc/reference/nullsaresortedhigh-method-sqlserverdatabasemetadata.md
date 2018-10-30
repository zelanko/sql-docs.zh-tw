---
title: nullsAreSortedHigh 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullsAreSortedHigh
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ff97d37-befc-47b1-8092-505917216a41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f5014ab32565e4be32d3611c472354f27d15460
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835066"
---
# <a name="nullsaresortedhigh-method-sqlserverdatabasemetadata"></a>nullsAreSortedHigh 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出是否將 NULL 值排在最前面。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean nullsAreSortedHigh()  
```  
  
## <a name="return-value"></a>傳回值  
 如果將值排在最前面，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 nullsAreSortedHigh 方法是由 java.sql.DatabaseMetaData 介面中 nullsAreSortedHigh 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
