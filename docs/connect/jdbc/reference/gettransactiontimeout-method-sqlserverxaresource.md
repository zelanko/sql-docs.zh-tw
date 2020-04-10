---
title: getTransactionTimeout 方法 (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAResource.getTransactionTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed0a37e9-1132-4d3f-b88f-8be674e852b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cae91c04487f3ca973e9c7697ec992f61632ca17
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911337"
---
# <a name="gettransactiontimeout-method-sqlserverxaresource"></a>getTransactionTimeout 方法 (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  取得為這個 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件設定的目前交易逾時值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getTransactionTimeout()  
```  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>備註  
 這個 getTransactionTimeout 方法是由 javax.transaction.xa.XAResource 介面中的 getTransactionTimeout 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
