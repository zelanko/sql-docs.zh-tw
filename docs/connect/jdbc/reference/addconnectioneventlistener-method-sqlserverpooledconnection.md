---
description: addConnectionEventListener 方法 (SQLServerPooledConnection)
title: addConnectionEventListener 方法 (SQLServerPooledConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPooledConnection.addConnectionEventListener
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 142830a8-8d4e-48ca-911d-85bf195ca4fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f0fbbcfd24d4dee568745f727c027d5ea8fda0d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438240"
---
# <a name="addconnectioneventlistener-method-sqlserverpooledconnection"></a>addConnectionEventListener 方法 (SQLServerPooledConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  註冊指定的事件接聽程式，如此一來，當這個 [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md) 物件上發生事件時，它就可以收到通知。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void addConnectionEventListener(javax.sql.ConnectionEventListener listener)  
```  
  
#### <a name="parameters"></a>參數  
 *listener*  
  
 ConnectionEventListener 物件。  
  
## <a name="remarks"></a>備註  
 這個 addConnectionEventListener 方法是由 javax.sql.PooledConnection 介面中的 addConnectionEventListener 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerPooledConnection 方法](../../../connect/jdbc/reference/sqlserverpooledconnection-methods.md)   
 [SQLServerPooledConnection 成員](../../../connect/jdbc/reference/sqlserverpooledconnection-members.md)   
 [SQLServerPooledConnection 類別](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
  
