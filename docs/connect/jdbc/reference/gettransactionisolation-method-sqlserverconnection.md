---
title: getTransactionIsolation 方法 (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getTransactionIsolation
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 179772e9-6572-4ce5-83c5-ab2b196cee67
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b7636b1987a6b210af06436dee4b7a9ad788f2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911403"
---
# <a name="gettransactionisolation-method-sqlserverconnection"></a>getTransactionIsolation 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取這個 [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) 物件的目前交易隔離等級。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getTransactionIsolation()  
```  
  
## <a name="return-value"></a>傳回值  
 **int** 值，包含下列其中一個隔離等級：  
  
 TRANSACTION_NONE  
  
 TRANSACTION_READ_UNCOMMITTED  
  
 TRANSACTION_READ_COMMITTED  
  
 TRANSACTION_REPEATABLE_READ  
  
 TRANSACTION_SERIALIZABLE  
  
 TRANSACTION_SNAPSHOT = 0x1000  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 這個 getTransactionIsolation 方法是由 java.sql.Connection 介面中的 getTransactionIsolation 方法所指定。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
