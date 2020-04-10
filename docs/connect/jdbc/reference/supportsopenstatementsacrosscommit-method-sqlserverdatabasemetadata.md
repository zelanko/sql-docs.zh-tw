---
title: supportsOpenStatementsAcrossCommit 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenStatementsAcrossCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e733586c-9222-43cb-92ea-ba474f442a43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb6d7af696e04114b4eb44b11145ea1f0c4edfcf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928512"
---
# <a name="supportsopenstatementsacrosscommit-method-sqlserverdatabasemetadata"></a>supportsOpenStatementsAcrossCommit 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援在所有認可之間維持陳述式為開啟狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsOpenStatementsAcrossCommit()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsOpenStatementsAcrossCommit 方法是由 java.sql.DatabaseMetaData 介面中的 supportsOpenStatementsAcrossCommit 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
