---
title: 已啟用 Azure Arc 的 SQL Server - 版本資訊
description: 最新版本資訊
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/29/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3dcbc6b17d5abe87aabe923d70746d65595b9de6
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244650"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>版本資訊 - 已啟用 Azure Arc 的 SQL Server (預覽)

> [!NOTE]
> 作為預覽功能，本文所述的技術受限於 [Microsoft Azure 預覽版增補使用規定](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。

## <a name="september-2020"></a>2020 年 9 月

已啟用 Azure Arc 的 SQL Server 發行公開預覽。 已啟用 Azure Arc 的 SQL Server 將 Azure 服務擴充至 SQL Server 執行個體，該執行個體裝載於客戶資料中心的 Azure 外部、邊緣或多重雲端環境中。

如需詳細資料，請參閱[已啟用 Azure Arc 的 SQL Server 概觀](overview.md)

### <a name="known-issues"></a>已知問題

下列問題適用於 9 月版本：

* [註冊已啟用 Azure Arc 的 SQL Server] 刀鋒視窗不支援設定自訂標籤。 若要新增自訂標籤，請在註冊後開啟 [SQL Server - Azure Arc] 資源，並在 [概觀] 頁面中變更 [標籤]。

* 將 SQL Server 執行個體連線到 Azure Arc 需要具有一組廣泛權限的帳戶。 如需詳細資料，請參閱[所需的權限](overview.md#required-permissions)。

## <a name="october-2020"></a>2020 年 10 月

10 月更新包含下列改善項目：

* [註冊已啟用 Azure Arc 的 SQL Server] 刀鋒視窗現在包含 [標籤] 索引標籤。這些標籤會包含在註冊指令碼中，並反映在 [SQL Server - Azure Arc] 資源中。 如需詳細資料，請參閱[將 SQL Server 連線到 Azure Arc](connect.md)。

* [Environment Health] \(環境健全狀況\) 項目現在支援藉由部署 *CustomScriptExtension* ，以從入口網站啟用 [SQL 評定]。 如需詳細資料，請參閱[設定 SQL 評定](assess.md#run-on-demand-sql-assessment)。

### <a name="known-issues"></a>已知問題

下列問題適用於 10 月版本：

* 將 SQL Server 執行個體連線到 Azure Arc 需要具有一組廣泛權限的帳戶。 如需詳細資料，請參閱[所需的權限](overview.md#required-permissions)。

## <a name="next-steps"></a>後續步驟

**只想試試看嗎？**  請參閱[已啟用 Azure Arc 的 SQL Server 快速入門](https://aka.ms/AzureArcSqlServerJumpstart)來快速開始使用。
