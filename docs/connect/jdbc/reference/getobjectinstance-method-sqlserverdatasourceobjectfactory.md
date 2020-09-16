---
description: getObjectInstance 方法 (SQLServerDataSourceObjectFactory)
title: getObjectInstance 方法 (SQLServerDataSourceObjectFactory) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79510f1e28f6f8933b417ad17ecac34713e885e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435060"
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance 方法 (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取指定之資料來源物件的執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>參數  
 *ref*  
  
 **Object** 值。  
  
 *name*  
  
 物件的名稱。  
  
 *c*  
  
 相對於指定之名稱的內容。  
  
 *h*  
  
 用於建立物件的環境。  
  
## <a name="return-value"></a>傳回值  
 **Object** 值。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>備註  
 這個 getObjectInstance 方法是由 javax.naming.spi.ObjectFactory 介面中的 getObjectInstance 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSourceObjectFactory 方法](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory 成員](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory 類別](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
