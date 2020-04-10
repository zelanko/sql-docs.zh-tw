---
title: supportsCatalogsInPrivilegeDefinitions 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInPrivilegeDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cc18f99e-c19f-4bd0-96ae-b9a6a0de1926
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8a897c22b5e6879c67e02a72fe1b7d342662363c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928621"
---
# <a name="supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata"></a>supportsCatalogsInPrivilegeDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出目錄名稱是否可以用於權限定義陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsCatalogsInPrivilegeDefinitions()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsCatalogsInPrivilegeDefinitions 方法是由 java.sql.DatabaseMetaData 介面中的 supportsCatalogsInPrivilegeDefinitions 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
