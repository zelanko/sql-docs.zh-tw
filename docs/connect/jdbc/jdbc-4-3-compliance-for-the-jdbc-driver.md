---
title: JDBC 4.3 合規性的 JDBC 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f529c88044444f3fb6e428b6c69f5a5cf5917251
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278909"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC Driver 的 JDBC 4.3 合規性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  適用於 SQL Server 的 Microsoft JDBC Driver 6.4 之前的版本，與 Java 資料庫連線 (JDBC) API 4.2 規格相容。 本節不適用於 6.4 版之前的版本。  
  
 從 6.4 版開始，Microsoft JDBC Driver for SQL Server 是 JAVA 10 相容，但它不是完全符合 JDBC API 4.3 規格。 驅動程式中，會擲回 SQLFeatureNotSupportedException 未實作方法。 
 
 下列的 JDBC 4.3 API 方法會實作 Microsoft JDBC Driver 6.4 for SQL Server。
 
  **SQLServerConnection 類別**  
  
|新的方法|Description|值得注意的實作|  
|-----------------|-----------------|-------------------------------|  
|void beginrequest （)|驅動程式的要求，而獨立的工作單位，從這個連接上的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|儲存是透過公用 API 方法，您可以修改連接欄位的值： `databaseAutoCommitMode`， `transactionIsolationLevel`， `networkTimeout`， `holdability`， `sendTimeAsDatetime`， `statementPoolingCacheSize`， `disableStatementPooling`， `serverPreparedStatementDiscardThreshold`， `enablePrepareOnFirstPreparedStatementCall `，`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void endRequest()|驅動程式的要求，而獨立的工作單位，已完成的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|關閉期間的工作單位所建立的陳述式，並回復任何開啟的交易。 方法也會還原以上所列的連線欄位所做的變更。|