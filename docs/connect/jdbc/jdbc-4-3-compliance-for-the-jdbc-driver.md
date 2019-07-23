---
title: JDBC Driver 的 JDBC 4.3 合規性 |Microsoft Docs
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
ms.openlocfilehash: 20cefb029a126b0a262d86a2dc0a0791959085bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956360"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC Driver 的 JDBC 4.3 合規性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Microsoft JDBC Driver 6.4 for SQL Server 以前的版本僅相容於 Java 資料庫連線 (JDBC) API 4.2 規格。 本節不適用於 6.4 版 (含) 以前的版本。

從6.4 版, Microsoft JDBC Driver for SQL Server 與 JAVA 9 相容, 並`SQLFeatureNotSupportedException`會擲回具有未實現方法的新 jdbc 4.3 api。

使用 Microsoft JDBC Driver 7.0 for SQL Server 版本, 此驅動程式現在與 JAVA 10 相容, 並支援以下所述的 Api。 驅動程式`SQLFeatureNotSupportedException`會針對 JDBC 4.3 規格中的其他未實現方法擲回。

|新增 API|Description|值得注意的實作|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|從這個連接開始, 要求 (獨立工作單位) 的驅動程式提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)。|儲存可透過`databaseAutoCommitMode`公用 API 方法修改的連接欄位的值:、 `serverPreparedStatementDiscardThreshold` `disableStatementPooling` `transactionIsolationLevel`、 `networkTimeout`、 `holdability`、 `sendTimeAsDatetime`、 `statementPoolingCacheSize`、 `enablePrepareOnFirstPreparedStatementCall`、、、`catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|要求 (獨立工作單位) 已完成之驅動程式的提示。 如需詳細資訊，請參閱 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)。|關閉在工作單位期間建立的語句, 並復原任何開啟的交易。 方法也會將變更還原至上列的連接欄位。|
