---
title: getXAResource 方法 (SQLServerXAConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerXAConnection.getXAResource
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d2828f-fd20-44b0-b796-dc70f77c5b03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d48ba821cee687eca112c405e5f0363244bc7842
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700136"
---
# <a name="getxaresource-method-sqlserverxaconnection"></a>getXAResource 方法 (SQLServerXAConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件，交易管理員將會使用它來管理參與分散式交易的這個 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public javax.transaction.xa.XAResource getXAResource()  
```  
  
## <a name="return-value"></a>傳回值  
 XAResource 物件。  
  
## <a name="exceptions"></a>例外狀況  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 這個 getXAResource 方法是由 javax.sql.XAConnection 介面中 getXAResource 方法指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 方法](../../../connect/jdbc/reference/sqlserverxaconnection-methods.md)   
 [SQLServerXAConnection 成員](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [SQLServerXAConnection 類別](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)  
  
  
