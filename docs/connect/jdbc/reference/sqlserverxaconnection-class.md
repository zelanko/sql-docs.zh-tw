---
title: SQLServerXAConnection 類別 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6563ca27d1e2abfbabf30374e410cdd970651d34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846343"
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
  
  
