---
title: SQLServerConnection 類別
description: 了解 JDBC Driver for SQL Server 中 SQLServerConnection 類別的公用 API 詳細資料。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 937292a6-1525-423e-a2b2-a18fd34c2893
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6827b79b4d1cc7b3f66db3c53c338614ec49fc3
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411474"
---
# <a name="sqlserverconnection-class"></a>SQLServerConnection 類別
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  代表與 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的 JDBC 連接。  
  
 **套件：** com.microsoft.sqlserver.jdbc  
  
 **實作：** [ISQLServerConnection](../../../connect/jdbc/reference/isqlserverconnection-interface.md)、java.io.Serializable  
  
## <a name="syntax"></a>語法  
  
```  
  
public class SQLServerConnection  
```  
  
## <a name="remarks"></a>備註  
 SQLServerConnection 支援 JDBC 連接共用，而且可以是實體 JDBC 連線或邏輯 JDBC 連線。 SQLServerConnection 會針對透過它建立的所有陳述式管理其交易控制，而且可以參與透過 XAResource 配接器所管理的 XA 分散式交易。  
  
 SQLServerConnection 會管理備妥陳述式控制代碼的集區。 備妥的陳述式只需準備一次，通常就可以針對其參數使用不同的資料值來執行多次。 備妥的陳述式也會在不同的邏輯 (共用) 連接關閉之間維護。  
  
> [!NOTE]  
>  SQLServerConnection 不是安全執行緒。 但是，從單一連接建立的多個陳述式可以同時在並行執行緒內處理。  
  
 這個類別支援解除包裝為 SQLServerConnection 類別、java.sql.connection 介面和 ISQLServerConnection 介面。 如需詳細資訊，請參閱[包裝函式與介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [JDBC 驅動程式 API 參考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
