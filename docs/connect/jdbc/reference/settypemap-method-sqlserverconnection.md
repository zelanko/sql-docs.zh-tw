---
title: setTypeMap 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setTypeMap
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bffd20a6-1310-44b0-9602-974500481fa6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a188d5d98aca0418a2452f29912f62604f3ffa90
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972167"
---
# <a name="settypemap-method-sqlserverconnection"></a>setTypeMap 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  安裝所指定 TypeMap object 物件來作為這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的類型對應。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 目前不支援這個方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setTypeMap(java.util.Map map)  
```  
  
#### <a name="parameters"></a>參數  
 *map*  
  
 TypeMap 物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 setTypeMap 方法是由 java.sql.Connection 介面中的 setTypeMap 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
