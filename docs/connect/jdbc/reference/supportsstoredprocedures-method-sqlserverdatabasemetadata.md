---
title: supportsStoredProcedures 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsStoredProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 776ff53a-8bf3-4864-a7b7-170fdef1a87b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86e425d40a12e441e1951962cac71152a21a7f69
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920705"
---
# <a name="supportsstoredprocedures-method-sqlserverdatabasemetadata"></a>supportsStoredProcedures 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援使用預存程序逸出語法的預存程序呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsStoredProcedures()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsStoredProcedures 方法是由 java.sql.DatabaseMetaData 介面中的 supportsStoredProcedures 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
