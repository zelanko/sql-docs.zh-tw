---
title: SQLServerXADataSource 類別 |Microsoft 文件
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
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb52f851b776b14c99ba98d64fabfc964b8029cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 factory [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md)為內部使用的物件。  
  
 **封裝：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **實作：** javax.sql.XADataSource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>備註  
 實作 SQLServerXADataSource 介面的物件通常會向使用 Java Naming and Directory Interface (JNDI) 的命名服務。  
  
 SQLServerXADataSource 類別會提供資料庫連接，以便用於分散式 (XA) 交易。 SQLServerXADataSource 類別也支援實體連接的連接共用。 SQLServerXADataSource 和 SQLServerXAConnection 介面，定義於 javax.sql 封裝內，由實作[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]。  
  
 SQLServerXAConnection 物件是共用的連接可參與分散式交易。 更明確地說，SQLServerXAConnection SQLServerPooledConnection 介面藉由加入擴充方法[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)。 這個方法會產生[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)物件，可以由交易管理員用來協調分散式交易中的其他參與者這個連接上完成的工作。 因為它們會擴充 SQLServerPooledConnection 介面，SQLServerXAConnection 物件支援 SQLServerPooledConnection 物件的所有方法。 這些是與基礎資料來源之間的可重複使用的實體連接，而且會產生可以傳回到 JDBC 應用程式的實體連接控制代碼。  
  
 SQLServerXAConnection 物件是由 SQLServerXADataSource 物件所產生。 SQLServerConnectionPoolDataSource 物件和 SQLServerXADataSource 物件是類似，因為兩者都是 JDBC 應用程式可以看到資料來源層底下來實作它們。 此架構可讓[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]對應用程式是透明的方式支援分散式的交易。 SQLServerXADataSource 可以設定為與整合[!INCLUDE[msCoName](../../../includes/msconame_md.md)]藉此提供真正的分散式交易協調器 (DTC) 的分散式交易處理。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXADataSource 成員](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
