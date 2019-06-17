---
title: SQLServerXAConnection 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 177b10c9657c4cb8d6b37f7dec9d3b860308dcb7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788900"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表可以參與分散式 (XA) 交易的 JDBC 連接。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **實作：** javax.sql.XAConnection  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerXAConnection 物件可以透過 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件登錄在分散式交易中。 交易管理員，通常屬於中間層伺服器，管理透過 SQLServerXAResource 物件 SQLServerXAConnection 物件。  
  
> [!NOTE]  
>  應用程式設計人員通常不會直接使用這個介面。 它主要是由在中間層伺服器工作的交易管理員所使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 成員](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
