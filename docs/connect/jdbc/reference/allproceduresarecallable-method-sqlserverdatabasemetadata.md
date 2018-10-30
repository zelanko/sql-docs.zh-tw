---
title: allProceduresAreCallable 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allProceduresAreCallable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8886137d-455e-497c-afea-4b326eda52f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ae9cc9bc9634131c197f634c713125f23ddd86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790326"
---
# <a name="allproceduresarecallable-method-sqlserverdatabasemetadata"></a>allProceduresAreCallable 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出目前使用者是否有權限可以呼叫由 [getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md) 方法傳回的所有程序。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean allProceduresAreCallable()  
```  
  
## <a name="return-value"></a>傳回值  
 如果使用者有權限可呼叫所有程序，則為 **true**； 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 allProceduresAreCallable 方法是由 java.sql.DatabaseMetaData 介面中 allProceduresAreCallable 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
