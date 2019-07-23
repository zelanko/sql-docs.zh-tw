---
title: supportsSchemasInPrivilegeDefinitions 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSchemasInPrivilegeDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2957af1d-62d6-4375-b214-bbba9aafcc2d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e02efacfad43c840550d6638dde4f46a59b399f5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968890"
---
# <a name="supportsschemasinprivilegedefinitions-method-sqlserverdatabasemetadata"></a>supportsSchemasInPrivilegeDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出結構描述名稱是否可以用於權限定義陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsSchemasInPrivilegeDefinitions()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援,**則為 true** 。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 supportsSchemasInPrivilegeDefinitions 方法是由 JAVA.sql.databasemetadata 介面中的 supportsSchemasInPrivilegeDefinitions 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
