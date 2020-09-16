---
description: getMaxSchemaNameLength 方法 (SQLServerDatabaseMetaData)
title: getMaxSchemaNameLength 方法 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxSchemaNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fece19e9-3bf8-4299-9188-ac3df5ce9c19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6afda7245d68adc5698fd4934d374552841d073d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435510"
---
# <a name="getmaxschemanamelength-method-sqlserverdatabasemetadata"></a>getMaxSchemaNameLength 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個資料庫允許在結構描述名稱中使用的最大字元數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getMaxSchemaNameLength()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，指出允許的最大字元數。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getMaxSchemaNameLength 方法是由 java.sql.DatabaseMetaData 介面中的 getMaxSchemaNameLength 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成員](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 類別](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
