---
title: SQLServerXADataSource 類別 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4c456336170cd7d4ad7cf37a0eebc52637f0a070
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970229"
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表內部使用之 [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) 物件的 Factory。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **實作：** javax.sql.XADataSource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>Remarks  
 實作 SQLServerXADataSource 介面的物件，通常會向使用 Java Naming and Directory Interface (JNDI) 的命名服務註冊。  
  
 SQLServerXADataSource 類別會提供資料庫連線，以便用於分散式 (XA) 交易。 SQLServerXADataSource 類別也支援實體連接的連接共用。 SQLServerXADataSource 和 SQLServerXAConnection 介面 (定義于封裝 javax.xml.transform.dom.domresult 中) 是由[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]所執行。  
  
 SQLServerXAConnection 物件是可以參與分散式交易的共用連線。 更精確地說, SQLServerXAConnection 會藉由新增方法[getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md)來擴充 SQLServerPooledConnection 介面。 這個方法會產生 [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) 物件，交易管理員可以使用這個物件來與分散式交易其他參與者協調在這個連線上完成的工作。 因為它們會擴充 SQLServerPooledConnection 介面, 所以 SQLServerXAConnection 物件支援 SQLServerPooledConnection 物件的所有方法。 這些是與基礎資料來源之間的可重複使用的實體連接，而且會產生可以傳回到 JDBC 應用程式的實體連接控制代碼。  
  
 SQLServerXAConnection 物件是由 SQLServerXADataSource 物件所產生。 SQLServerConnectionPoolDataSource 物件和 SQLServerXADataSource 物件很相似, 因為它們都是在 JDBC 應用程式可見的資料來源層底下執行。 此架構可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用對應用程式而言透明的方式支援分散式交易。 SQLServerXADataSource 可以設定為與整合 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 分散式交易協調器 (DTC)，藉此提供真正的分散式交易處理。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerXADataSource 成員](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
