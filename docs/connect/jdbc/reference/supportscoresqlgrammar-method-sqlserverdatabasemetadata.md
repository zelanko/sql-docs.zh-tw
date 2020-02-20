---
title: supportsCoreSQLGrammar 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCoreSQLGrammar
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6b82f300-f906-4d11-b810-525bda4a88ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73cbbaf8d1a3b3e6bc5e5ba7cd4b43df01c0f7f1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969590"
---
# <a name="supportscoresqlgrammar-method-sqlserverdatabasemetadata"></a>supportsCoreSQLGrammar 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出這個資料庫是否支援 ODBC Core SQL 文法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsCoreSQLGrammar()  
```  
  
## <a name="return-value"></a>傳回值  
 如果支援，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 supportsCoreSQLGrammer 方法是由 java.sql.DatabaseMetaData 介面中的 supportsCoreSQLGrammer 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
