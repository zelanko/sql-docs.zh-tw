---
description: SQLServerClob 建構函式 (SQLServerConnection, java.lang.String)
title: SQLServerClob 建構函式 (SQLServerConnection, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.SQLServerClob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7058f4f7-ef3e-4d62-90d1-79299708b1eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ea4bec9b1d3bc8ab297d548dfb8c94f4007d861
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478591"
---
# <a name="sqlserverclob-constructor-sqlserverconnection-javalangstring"></a>SQLServerClob 建構函式 (SQLServerConnection, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當指定 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件和資料字串時，初始化 [SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md) 類別的新執行個體。  
  
> [!NOTE]  
>  這個方法在 JDBC Driver 2.0 版中已被取代。 請改用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md) 方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public SQLServerClob(SQLServerConnection connection,  
                     java.lang.String data)  
```  
  
#### <a name="parameters"></a>參數  
 *connection*  
  
 SQLServerConnection 物件。  
  
 *data*  
  
 CLOB 資料。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerClob 建構函式](../../../connect/jdbc/reference/sqlserverclob-constructors.md)   
 [SQLServerClob 成員](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 類別](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
