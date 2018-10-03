---
title: supportsCatalogsInTableDefinitions 方法 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInTableDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e1e50ac-f3d4-416a-8a69-d8b7b4f30bf3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c57bf4585c621093acf2ba41d7e12bd44be4557
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616959"
---
# <a name="supportscatalogsintabledefinitions-method-sqlserverdatabasemetadata"></a>supportsCatalogsInTableDefinitions 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，此值指出目錄名稱是否可以用於資料表定義陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean supportsCatalogsInTableDefinitions()  
```  
  
## <a name="return-value"></a>傳回值  
 **true**如果支援。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 這個 supportsCatalogsInTableDefinitions 方法是由 java.sql.DatabaseMetaData 介面中 supportsCatalogsInTableDefinitions 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
