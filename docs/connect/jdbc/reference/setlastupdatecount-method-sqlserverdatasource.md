---
title: setLastUpdateCount 方法 (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3369fbc84cb16ed0f9b587ed20fe7fe368d11b02
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2018
ms.locfileid: "49084907"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>setLastUpdateCount 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定 **Boolean** 值，這個值會指出是否啟用 lastUpdateCount 屬性。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>參數  
 *lastUpdateCount*  
  
 如果啟用 lastUpdateCount 屬性，則為 **true**； 否則為 **false**。  
  
## <a name="remarks"></a>Remarks  
 如果 lastUpdateCount 屬性設定為 **true**[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 就只會從傳遞至伺服器的 SQL 陳述式傳回上次更新計數。 如果 lastUpdateCount 屬性設定為 **false**，則此驅動程式將傳回所有更新計數，包括任何可能已引發之觸發程序所傳回的更新計數。 如果未設定 lastUpdateCount 屬性，[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md) 方法會傳回預設值 **true**。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
