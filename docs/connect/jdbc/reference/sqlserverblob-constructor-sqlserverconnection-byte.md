---
description: SQLServerBlob 建構函式 (SQLServerConnection, byte)
title: SQLServerBlob 建構函式 (SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 968c32094196c88ab8eb607e6faa8992de40ed00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472160"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob 建構函式 (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  當給定 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件和**位元組**陣列時，初始化 [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) 類別的新執行個體。  
  
> [!NOTE]  
>  這個方法在 JDBC Driver 2.0 版中已被取代。 請改用 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 類別的 [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) 方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>參數  
 *connection*  
  
 SQLServerConnection 物件。  
  
 *data*  
  
 **位元組**陣列。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerBlob 建構函式](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [SQLServerBlob 成員](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob 類別](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
