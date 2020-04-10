---
title: getMaxColumnsInTable 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxColumnsInTable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dbcad2e1-7508-49ff-9f6d-db11200d87b6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7669992b74bbb8b2291a657bb35dadb51a3ec383
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80907054"
---
# <a name="getmaxcolumnsintable-method-sqlserverdatabasemetadata"></a>getMaxColumnsInTable 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在資料表中使用的最大資料行數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxColumnsInTable()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大資料行數目。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxColumnsInTable 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxColumnsInTable 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
