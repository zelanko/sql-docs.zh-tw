---
title: getDatabaseProductVersion 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDatabaseProductVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19c0c15d-223f-45bd-a215-2867dfefecb0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd09db3880b7e4294620f9e8f0476fc759d1a54a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923201"
---
# <a name="getdatabaseproductversion-method-sqlserverdatabasemetadata"></a>getDatabaseProductVersion 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫產品的版本號碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.String getDatabaseProductVersion()  
```  
  
## <a name="return-value"></a>傳回值  
 包含資料庫產品版本號碼的**字串**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getDatabaseProductVersion 方法是由 java.sql.DatabaseMetaData 介面中的 getDatabaseProductVersion 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
