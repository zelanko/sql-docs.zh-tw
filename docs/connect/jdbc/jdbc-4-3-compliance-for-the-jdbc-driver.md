---
title: 適用於 JDBC 驅動程式的 JDBC 4.3 合規性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed9b10ad9e9a927789505c7d7327c6cf4d1ff3c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027938"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>適用於 JDBC 驅動程式的 JDBC 4.3 合規性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Microsoft JDBC Driver 6.4 for SQL Server 以前的版本僅相容於 Java 資料庫連線 (JDBC) API 4.2 規格。 本節不適用於 6.4 版 (含) 以前的版本。

與 6.4 版一樣，Microsoft JDBC Driver for SQL Server 與 JAVA 9 相容，而且會針對具有未實作方法的新 JDBC 4.3 API 擲回 `SQLFeatureNotSupportedException`。

從 Microsoft JDBC Driver 7.0 for SQL Server 版本開始，驅動程式現在已經與 JAVA 10 相容，而且支援以下所述的 API。 驅動程式會針對 JDBC 4.3 規格中其他未實作的方法擲回 `SQLFeatureNotSupportedException`。

|新增 API|描述|值得注意的實作|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|從這個連線開始，驅動程式要求要有一個獨立工作單位的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|儲存可透過公用 API 方法修改的連線欄位值：`databaseAutoCommitMode`、`transactionIsolationLevel`、`networkTimeout`、`holdability`、`sendTimeAsDatetime`、`statementPoolingCacheSize`、`disableStatementPooling`、`serverPreparedStatementDiscardThreshold`、`enablePrepareOnFirstPreparedStatementCall`、`catalogName`、`sqlWarnings`、`useBulkCopyForBatchInsert`。|
|void java.sql.connection.endRequest()|要求獨立工作單位的驅動程式已完成的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|關閉在工作單位期間建立的陳述式，並復原任何開啟的交易。 該方法也會將變更還原至上面列出的連線欄位。|
