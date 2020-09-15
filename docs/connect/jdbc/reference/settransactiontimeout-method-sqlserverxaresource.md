---
description: setTransactionTimeout 方法 (SQLServerXAResource)
title: setTransactionTimeout 方法 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.setTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38bf4a1a-6ad3-437c-b9ed-8792ab6dde7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21c1771f0911bb3bf0fa91c0f1356b82fad2348f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354964"
---
# <a name="settransactiontimeout-method-sqlserverxaresource"></a>setTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定這個 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件的目前交易逾時值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public boolean setTransactionTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>參數  
 *seconds*  
  
 **int** 值。  
  
## <a name="return-value"></a>傳回值  
 如果已成功設定逾時，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 此 setTransactionTimeout 方法是由 javax.transaction.xa.XAResource 介面中的 setTransactionTimeout 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
