---
description: rollback 方法 ()
title: rollback 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7adb6772-4047-4d8e-931d-b3d20eec44b5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca2a2847f9d917872ee3a0b56bad50b184f58ea2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432670"
---
# <a name="rollback-method-"></a>rollback 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  復原目前交易中所做的所有變更，並釋放目前由這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件保留的所有資料庫鎖定。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void rollback()  
```  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 rollBack 方法是由 java.sql.Connection 介面中的 rollBack 方法指定。  
  
 只有當已經停用自動認可模式時，才應該使用這個方法。  
  
## <a name="see-also"></a>另請參閱  
 [rollback 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
