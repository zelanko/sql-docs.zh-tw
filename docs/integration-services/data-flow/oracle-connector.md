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
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553238"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Oracle 能讓您以 SSIS 套件將資料從 Oracle 資料來源匯出，或將資料匯入其中。

## <a name="version-support"></a>版本支援

Microsoft Connector for Oracle 支援下列 Microsoft SQL Server 產品：

- 自 SQL Server 2019 起
- SQL Server Data Tools (SSDT)

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

如果您需要在 SQL Server 中執行套件，您可以從[這裡](https://www.microsoft.com/en-us/download/details.aspx?id=58228) \(英文\) 取得 Microsoft Connector for Oracle Database 安裝程式。 然後，遵循安裝精靈中的指示進行。

安裝連接器之後，您必須重新啟動 SQL Server Integration Service，以確保 Oracle 來源和目的地能正常運作。

如果您需要使用連接器來設計套件，則不需要下載連接器。 SQL Server Data Tools (SSDT) 自 15.9.0 版以來已包含該檔案。

## <a name="uninstallation"></a>解除安裝

您可以執行解除安裝精靈來將 Microsoft Connector for Oracle Database 從 SQL Server 移除。

## <a name="design-ssis-package-with-previous-version"></a>使用舊版來設計 SSIS 套件

自 15.9.0 版以來，SSDT 已經包含 Microsoft Connector for Oracle Database，因此在設計以 SQL Server 2019 為目標的 SSIS 套件時，您不需要進行任何安裝。

若要設計以 SQL Server 2017 和以下版本為目標的 SSIS 套件，您需要安裝相對應版本的 Connector for Oracle by Attunity。

**下載連結：**

- [SQL Server 2017：Microsoft Connector Version 5.0 for Oracle by Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=55179) \(英文\)
- [SQL Server 2016：Microsoft Connector Version 4.0 for Oracle by Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=52950) \(英文\)
- [SQL Server 2014：Microsoft Connector Version 3.0 for Oracle by Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=44582) \(英文\)
- [SQL Server 2012：Microsoft Connector Version 2.0 for Oracle by Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=29283) \(英文\)

## <a name="next-steps"></a>後續步驟

- 設定 [Oracle 連線管理員](oracle-connection-manager.md)。
- 設定 [Oracle 來源](oracle-source.md)。
- 設定 [Oracle 目的地](oracle-destination.md)。
- 如有任何疑問，請瀏覽 [TechCommunity](https://aka.ms/AA5u35j) \(英文\)。
