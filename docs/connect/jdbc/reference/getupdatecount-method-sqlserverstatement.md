---
description: getUpdateCount 方法 (SQLServerStatement)
title: getUpdateCount 方法 (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e9570228-4500-44b6-b2f1-84ac050b5112
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19a4cfc7b9957d8ba4392477e6dcd3732f10bd7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433900"
---
# <a name="getupdatecount-method-sqlserverstatement"></a>getUpdateCount 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取目前結果當做更新計數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final int getUpdateCount()  
```  
  
## <a name="return-value"></a>傳回值  
 **int**，包含更新計數。 如果傳回的結果是結果集物件或者沒有其他結果，則會傳回 -1。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getUpdateCount 方法是由 java.sql.Statement 介面中的 getUpdateCount 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
