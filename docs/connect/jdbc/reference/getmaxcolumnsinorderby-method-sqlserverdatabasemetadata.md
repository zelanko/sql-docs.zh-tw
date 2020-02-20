---
title: getMaxColumnsInOrderBy 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInOrderBy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d6af9bb4-c55d-41f4-a266-d10ebee61194
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 60bb089d5c53699cda93c888b959fe71e5ffbfe6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982236"
---
# <a name="getmaxcolumnsinorderby-method-sqlserverdatabasemetadata"></a>getMaxColumnsInOrderBy 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在 ORDER BY 子句中使用的最大資料行數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxColumnsInOrderBy()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大資料行數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxColumnsInOrderBy 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxColumnsInOrderBy 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
