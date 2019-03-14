---
title: JDBC 4.3 合規性的 JDBC 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc2fbb2b217880b255d522149dabd38701a8c0e4
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579058"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC Driver 的 JDBC 4.3 合規性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Microsoft JDBC Driver 6.4 for SQL Server 以前的版本僅相容於 Java 資料庫連線 (JDBC) API 4.2 規格。 本節不適用於 6.4 版 (含) 以前的版本。

從 6.4 版開始，Microsoft JDBC Driver for SQL Server JAVA 9 相容，而且會擲回`SQLFeatureNotSupportedException`針對新的 JDBC 4.3 Api，有未提供的方法。

使用 Microsoft JDBC Driver for SQL Server 版本 7.0，驅動程式現在是 JAVA 10 相容，而且支援以下所述的 Api。 驅動程式會擲回`SQLFeatureNotSupportedException`其他未實作的方法，從 JDBC 4.3 規格。

|新的 API|Description|值得注意的實作|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|驅動程式的要求，而獨立的工作單位，從這個連接上的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|儲存是透過公用 API 方法，您可以修改連接欄位的值： `databaseAutoCommitMode`， `transactionIsolationLevel`， `networkTimeout`， `holdability`， `sendTimeAsDatetime`， `statementPoolingCacheSize`， `disableStatementPooling`， `serverPreparedStatementDiscardThreshold`， `enablePrepareOnFirstPreparedStatementCall`，`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|驅動程式的要求，而獨立的工作單位，已完成的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|關閉期間的工作單位所建立的陳述式，並回復任何開啟的交易。 方法也會還原以上所列的連線欄位所做的變更。|
