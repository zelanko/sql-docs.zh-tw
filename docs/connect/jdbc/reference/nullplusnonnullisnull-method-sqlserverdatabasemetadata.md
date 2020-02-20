---
title: nullPlusNonNullIsNull 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.nullPlusNonNullIsNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c594736f-3a9b-463f-bbd8-eaf9221230ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 314c3bd05db19d795ce203308b9a9ab87a10e338
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976735"
---
# <a name="nullplusnonnullisnull-method-sqlserverdatabasemetadata"></a>nullPlusNonNullIsNull 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指出這個資料庫是否支援在 NULL 和非 NULL 值之間的串連為 NULL。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean nullPlusNonNullIsNull()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援串連，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 nullPlusNonNullIsNull 方法是由 java.sql.DatabaseMetaData 介面中的 nullPlusNonNullIsNull 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
