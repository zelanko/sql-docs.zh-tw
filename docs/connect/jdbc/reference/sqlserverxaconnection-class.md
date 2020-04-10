---
title: SQLServerXAConnection 類別 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5ecb4bf1-b8d1-47cf-9cb1-7a18acc11ce2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5503084440427c43989a740e9197423fc5438aa
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926953"
---
# <a name="sqlserverxaconnection-class"></a>SQLServerXAConnection 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表可以參與分散式 (XA) 交易的 JDBC 連接。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **延伸：** [SQLServerPooledConnection](../../../connect/jdbc/reference/sqlserverpooledconnection-class.md)  
  
 **實作：** javax.sql.XAConnection  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXAConnection  
```  
  
## <a name="remarks"></a>備註  
 SQLServerXAConnection 物件可以透過 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件登錄在分散式交易中。 通常屬於中介層伺服器之一部分的交易管理員會透過 SQLServerXAResource 物件管理 SQLServerXAConnection 物件。  
  
> [!NOTE]  
>  應用程式設計人員通常不會直接使用這個介面。 它主要是由在中間層伺服器工作的交易管理員所使用。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXAConnection 成員](../../../connect/jdbc/reference/sqlserverxaconnection-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
