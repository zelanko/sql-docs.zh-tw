---
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ca25b7425ce74cea820e295a6a99bc3a3c1e2817
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755850"
---
# <a name="microsoft-connector-for-teradata-preview"></a>Microsoft Connector for Teradata (預覽)
[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Teradata 能讓您以 SSIS 套件將資料從 Teradata 資料庫匯出，並將資料載入到其中。

這個新的連接器支援已啟用 1MB 資料表的資料庫。

## <a name="version-support"></a>版本支援

Microsoft Connector for Teradata 支援下列 Microsoft SQL Server 產品：

- Microsoft SQL Server 2019
- Microsoft SQL Server Data Tools (SSDT)

Microsoft Connector for Teradata 會使用 Teradata Parallel Transporter 應用程式設計語言介面，從 Teradata 資料庫載入及匯出資料。 下面是支援的版本：

- Teradata Parallel Transporter (Teradata PT) 16.10
- Teradata Parallel Transporter (Teradata PT) 16.20

以下是支援的資料來源 Teradata 資料庫版本：

- Teradata 資料庫 16.20
- Teradata 資料庫 16.10
- Teradata 資料庫 15.10
- Teradata 資料庫 15.00

如需 Teradata Parallel Transporter 應用程式設計介面程式設計人員指南的詳細資訊，請參閱 [Teradata 文件](https://docs.teradata.com/)。

## <a name="installation"></a>安裝

### <a name="prerequisite"></a>必要條件

在 32 位元電腦上，從 [Teradata 工具和公用程式 - Windows 安裝套件](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)安裝下列驅動程式：

- Teradata ODBC 驅動程式 (32 位元)
- Teradata PT API (32 位元)

在 64 位元電腦上，安裝下列驅動程式：

- Teradata ODBC 驅動程式 (64 位元)
- Teradata PT API (64 位元)

若要安裝 Teradata 資料庫的連接器，請從[最新版本的 Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599) 下載並執行安裝程式。 然後，遵循安裝精靈中的指示進行。

安裝連接器之後，您必須重新啟動 SQL Server Integration Service，以確保 Teradata 來源和目的地能正常運作。

若要執行以 SQL Server 2017 和以下版本為目標的 SSIS 套件，您需要從下列連結安裝相對應版本的 **Microsoft Connector for Teradata by Attunity**：

- [SQL Server 2017：Microsoft Connector Version 5.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016：Microsoft Connector Version 4.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014：Microsoft Connector Version 3.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012：Microsoft Connector Version 2.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>解除安裝

您可以執行解除安裝精靈來將 **Microsoft Connector for Teradata** 移除。

## <a name="next-steps"></a>後續步驟

- 設定 [Teradata 連線管理員](teradata-connection-manager.md)
- 設定 [Teradata 來源](teradata-source.md)
- 設定 [Teradata 目的地](teradata-destination.md)
- 如有任何疑問，請瀏覽[技術社群](https://aka.ms/AA6iwdw)。
