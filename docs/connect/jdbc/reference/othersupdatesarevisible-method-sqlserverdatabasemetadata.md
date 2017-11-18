---
title: "othersUpdatesAreVisible 方法 (SQLServerDatabaseMetaData) |Microsoft 文件"
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
- SQLServerDatabaseMetaData.othersUpdatesAreVisible
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3615c01f-ae0b-42a7-92b5-e8770d841c45
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 37d83af5a39868007d79a8e2aeee9738abce396e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="othersupdatesarevisible-method-sqlserverdatabasemetadata"></a>othersUpdatesAreVisible 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出是否可看見其他人所完成的更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean othersUpdatesAreVisible(int type)  
```  
  
#### <a name="parameters"></a>參數  
 *type*  
  
 **Int** ，指出結果集類型，可以是下列值的其中一個定義於 java.sql.ResultSet 或 SQLServerResultSet 中：  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet 型別  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet 型別  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>傳回值  
 **true**如果可以看見的更新。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 othersUpdatesAreVisible 方法是由 java.sql.DatabaseMetaData 介面中 othersUpdatesAreVisible 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

