---
title: 包含檔案
description: 包含檔案
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: a443b615a6a04b588ed6dc84c6a8a4f6ed12e2f0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726752"
---
## <a name="specifying-application-intent"></a>指定應用程式意圖

您可以在連接字串中指定關鍵字 **ApplicationIntent**。 可指派的值為 **ReadWrite** 或 **ReadOnly**。 預設值為 **ReadWrite**。

當 **ApplicationIntent=ReadOnly** 時，用戶端會在連線時要求讀取工作負載。 伺服器會在連線期間以及在 **USE** 資料庫陳述式期間，強制執行此意圖。

**ApplicationIntent** 關鍵字不適用於舊版唯讀資料庫。  


#### <a name="targets-of-readonly"></a>ReadOnly 的目標

當連線選擇 **ReadOnly** 時，連線會指派給可能已因為資料庫存在的下列任何特殊設定：

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 資料庫可以允許或不允許 Always On 目標資料庫上的讀取工作負載。 此選擇是透過使用 **PRIMARY_ROLE** 與 **SECONDARY_ROLE** Transact-SQL 陳述式的 **ALLOW_CONNECTIONS** 子句來控制的。

- [異地複寫](/azure/sql-database/sql-database-geo-replication-overview)

- [讀取相應放大](/azure/sql-database/sql-database-read-scale-out)

如果沒有任何那些特殊目標可用，則會從一般資料庫讀取。

&nbsp;

**ApplicationIntent** 關鍵字可啟用「唯讀路由」  。


## <a name="read-only-routing"></a>唯讀路由

唯讀路由功能可確保資料庫之唯讀複本的可用性。 若要啟用唯讀路由，必須符合下列所有條件：

- 您必須連接到 AlwaysOn 可用性群組的可用性群組接聽程式。

- **ApplicationIntent** 連接字串關鍵字必須設為 **ReadOnly**。

- 可用性群組必須由資料庫管理員設定為啟用唯讀路由。

每個都使用唯讀路由的多個連線可能不會都連線到相同的唯讀複本。 資料庫同步處理的變更或伺服器路由組態的變更，可能會導致用戶端連接至不同的唯讀複本。 您可以確保所有唯讀要求都連線到相同的唯讀複本。 透過*不*將可用性群組接聽程式傳遞到 **Server** 連接字串關鍵字，以確保此相同性。 請改為指定唯讀執行個體的名稱。

唯讀路由連線到主要複本的時間可能會比較長。 等候較久是因為唯讀路由會先連線到主要複本，然後尋找最佳可用的可讀次要複本。 由於這些多步驟，您應該將登入逾時增加到至少 30 秒。