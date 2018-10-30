---
title: setTransactionTimeout 方法 (SQLServerXAResource) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81bf280397b2ba1ddac428eb12c882af2b31e1b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615506"
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
  
 **Int**值。  
  
## <a name="return-value"></a>傳回值  
 如果已成功設定逾時，則為 **true**。 否則為 **false**。  
  
## <a name="exceptions"></a>例外狀況  
 javax.transaction.xa.XAException  
  
## <a name="remarks"></a>Remarks  
 這個 setTransactionTimeout 方法是由 javax.transaction.xa.XAResource 介面中 setTransactionTimeout 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAResource 方法](../../../connect/jdbc/reference/sqlserverxaresource-methods.md)   
 [SQLServerXAResource 成員](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [SQLServerXAResource 類別](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
