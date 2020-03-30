---
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92aaf7c04d7a5e176fce4448b9d4f6172b541647
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75755845"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Oracle 能讓您以 SSIS 套件將資料從 Oracle 資料來源匯出，或將資料匯入其中。

## <a name="version-support"></a>版本支援

Microsoft Connector for Oracle 支援下列 Microsoft SQL Server 產品：

- 自 SQL Server 2019 起
- 從 15.9.3 版開始的 SQL Server Data Tools (SSDT)

以下是支援的資料來源 Oracle 資料庫版本：

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (不含 Windows 驗證支援)

所有作業系統和平台都支援 Oracle 資料庫。
> [!NOTE]
>
> SQL Server 2019 中的 Microsoft Connector for Oracle Database 不需要 Oracle 用戶端。

## <a name="installation"></a>安裝

若要安裝 Oracle 資料庫的連接器，請從[最新版本的 Microsoft Connector for Oracle](https://www.microsoft.com/download/details.aspx?id=58228) 下載並執行安裝程式。 然後，遵循安裝精靈中的指示進行。

安裝連接器之後，您必須重新啟動 SQL Server Integration Service，以確保 Oracle 來源和目的地可以正常運作。

若要執行以 SQL Server 2017 和以下版本為目標的 SSIS 套件，除了 **Microsoft Connector for Oracle** 以外，您還需要從下列連結安裝 **Oracle 用戶端**和相對應版本的 **Microsoft Connector for Oracle by Attunity**：

- [SQL Server 2017：Microsoft Connector Version 5.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=55179) \(英文\)
- [SQL Server 2016：Microsoft Connector Version 4.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=52950) \(英文\)
- [SQL Server 2014：Microsoft Connector Version 3.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=44582) \(英文\)
- [SQL Server 2012：Microsoft Connector Version 2.0 for Oracle by Attunity](https://www.microsoft.com/download/details.aspx?id=29283) \(英文\)

## <a name="uninstallation"></a>解除安裝

您可以執行解除安裝精靈來將 Microsoft Connector for Oracle Database 從 SQL Server 移除。

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 連線管理員](oracle-connection-manager.md)。
- 設定 [Oracle 來源](oracle-source.md)。
- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。
