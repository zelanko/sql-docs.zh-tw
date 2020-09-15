---
description: SQLServerConnectionPoolDataSource 類別
title: SQLServerConnectionPoolDataSource 類別 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2faa9b4df512d9b37bbba581353938120b85cbb1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354784"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>SQLServerConnectionPoolDataSource 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表連接集區管理員的實體資料庫連接。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **擴充：** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **實作：** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>備註  
 SQLServerConnectionPoolDataSource 通常會用於 Java Application Server 環境，這類環境支援內建連接共用，而且需要透過 ConnectionPoolDataSource 來提供實體連接，例如可以提供 JDBC 3.0 API 規格連接共用的 Java Platform 和 Enterprise Edition (Java EE) 等應用程式伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnectionPoolDataSource 成員](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
