---
title: "supportsSchemasInTableDefinitions 方法 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInTableDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3326b1b0-53e2-42ae-9ff7-98e8c7017ffa
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6182218c14b24a771203ad220eb5e8b642c1438b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="supportsschemasintabledefinitions-method-sqlserverdatabasemetadata"></a>supportsSchemasInTableDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出結構描述名稱是否可以用於資料表定義陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsSchemasInTableDefinitions()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**受支援。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsSchemasInTableDefinitions 方法是由 java.sql.DatabaseMetaData 介面中 supportsSchemasInTableDefinitions 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

