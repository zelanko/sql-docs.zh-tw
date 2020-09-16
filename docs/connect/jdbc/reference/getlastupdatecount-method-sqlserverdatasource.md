---
description: getLastUpdateCount 方法 (SQLServerDataSource)
title: getLastUpdateCount 方法 (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44b5b9c19b07479aaeae6eb400d3212accd3e5fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435770"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回 **Boolean** 值，這個值會指出是否啟用 lastUpdateCount 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>傳回值  
 如果啟用 lastUpdateCount 屬性，則為 **true**； 否則為 **false**。  
  
## <a name="remarks"></a>備註  
 如果 lastUpdateCount 屬性設定為 **true**，[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 就只會從傳遞至伺服器的 SQL 陳述式傳回上次更新計數。 如果 lastUpdateCount 屬性設定為 **false**，則此驅動程式將傳回所有更新計數，包括任何可能已引發之觸發程序所傳回的更新計數。 如果未設定 lastUpdateCount 屬性，getLastUpdateCount 方法會傳回預設值 **true**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
