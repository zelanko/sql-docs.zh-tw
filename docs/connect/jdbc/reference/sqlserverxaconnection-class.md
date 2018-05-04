---
title: SQLServerXAConnection 類別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba48701c441a75f0d7c6b7f78c964384c47f94e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表可以參與分散式 (XA) 交易的 JDBC 連接。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **實作：** javax.sql.XAConnection  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>備註  
 SQLServerXAConnection 物件可以藉由在分散式交易中編列[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件。 交易管理員，通常屬於中間層伺服器，管理透過 SQLServerXAResource 物件 SQLServerXAConnection 物件。  
  
> [!NOTE]  
>  應用程式設計人員通常不會直接使用這個介面。 它主要是由在中間層伺服器工作的交易管理員所使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 成員](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
