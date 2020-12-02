---
title: SqlClient 驅動程式支援生命週期
description: 包含產品支援週期資訊的頁面。
ms.date: 11/19/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 30155a584de4e22692601a1dcf9551a67d4f580f
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2020
ms.locfileid: "95011791"
---
# <a name="sqlclient-driver-support-lifecycle"></a>SqlClient 驅動程式支援生命週期

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft.Data.SqlClient 程式庫會遵循適用於所有版本的最新 .NET Core 支援原則。

[檢視 .NET Core 支援原則](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) \(英文\)

## <a name="microsoftdatasqlclient-release-cadence"></a>Microsoft.Data.SqlClient 發行步調

從 1.2 版開始，每隔六個月就會定期發行穩定的新 (GA) 版本，期間還會提供 2 到 3 個預覽版本。 專案關係人和維護人員將根據一些資格和客戶回應，來選擇長期支援 (LTS) 版本。

### <a name="release-life-cycles"></a>版本生命週期

| 版本 | 正式發行日期 | 最新修補程式版本 | 修補程式發行日期 | 支援層級  | 結束支援 |
| -- | -- | -- | -- | -- | -- |
| 2.1 | 2020 年 11 月 19 日 | 2.1.0 | 2020 年 11 月 19 日 | 目前 | |
| 2.0 | 2020 年 6 月 16 日 | 2.0.1 | 2020 年 8 月 25 日 | 目前 | |
| 1.1 | 2019 年 11 月 20 日 | 1.1.3 | 2020 年 5 月 15 日 | LTS | 2022 年 11 月 21 日 |
| 1.0 | 2019 年 8 月 28 日 | 1.0.19269.1 | 2019 年 9 月 26 日 | 目前 | 2020 年 2 月 20 日 |

### <a name="long-term-support-lts-releases"></a>長期支援 (LTS) 版本

LTS 版本會在初始版本之後的三年內受到支援。

### <a name="current-releases"></a>目前版本

目前版本會在後續的目前或 LTS 版本之後的三個月內受到支援。

## <a name="sql-version-compatibility-with-microsoftdatasqlclient"></a>SQL 版本與 Microsoft.Data.SqlClient 的相容性

|資料庫版本&nbsp;&#8594;<br />&#8595; 驅動程式版本|Azure SQL Database|Azure Synapse Analytics|Azure SQL 受控執行個體|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|
|---|---|---|---|---|---|---|---|---|
|2.1|是|是|是|是|是|是|是|是|
|2.0|是|是|是|是|是|是|是|是|
|1.1|是|是|是|是|是|是|是|是|
|1.0|是|是|是|是|是|是|是|是|
