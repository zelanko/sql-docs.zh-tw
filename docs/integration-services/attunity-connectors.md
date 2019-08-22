---
title: Microsoft Connectors for Oracle and Teradata by Attunity (SSIS) | Microsoft Docs
ms.date: 08/16/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ''
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2f7b6ebe42d98002627c170daaee00d4886804e8
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553190"
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>適用於 Integration Services (SSIS) 的 Microsoft Connectors for Oracle and Teradata by Attunity

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

> [!NOTE]
> 適用於 Oracle 與 Teradata 的 Atunity 連接器支援 SQL Server 2017 與較舊版本。
>
> 從 SQL Server 2019 開始，在這裡取得 Oracle 與 Teradata 的最新連接器：[Microsoft Connector for Oracle](data-flow/oracle-connector.md)

當您將 SSIS 套件中的資料載入或載出 Oracle 或 Teradata 時，您可以下載適用於 Integration Services 的 Attunity 連接器來最佳化效能。

## <a name="download-the-latest-attunity-connectors"></a>下載最新的 Attunity 連接器

在此取得最新版的連接器：  
[Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>問題 - 在 [SSIS 工具箱] 中看不到 Attunity 連接器

若要在 [SSIS 工具箱] 中看到 Attunity 連接器，您所安裝之連接器版本的目標 SQL Server 版本，一定要與安裝在您電腦上的 SQL Server Data Tools (SSDT) 版本相同 (您也可能安裝舊版連接器)。這項需求與您想要在 SSIS 專案和套件中設為目標的 SQL Server 版本無關。

例如，如果您已安裝最新版的 SSDT，您會有組建編號開頭為 14 的 SSDT 17 版。 這個版本的 SSDT 新增 SQL Server 2017 的支援。 若要在 SSIS 套件開發期間看到並使用 Attunity 連接器 (即使您想要以舊版 SQL Server 為目標亦然)，您還必須安裝最新版的 Attunity 連接器，也就是 5.0 版。 這個版本的連接器也新增 SQL Server 2017 的支援。

請從 [說明]   | [關於 Microsoft Visual Studio]  ，或在 [主控台] 的 [程式和功能]  中，查看 Visual Studio 中安裝的 SSDT 版本。 然後安裝下表中的對應 Attunity 連接器版本。

|SSDT 版本|SSDT 組建編號|目標 SQL Server 版本|所需的連接器版本|
|---------|---------|---------|---------|
|17|開頭為 14|SQL Server 2017|[Microsoft Connectors v5.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|開頭為 13|SQL Server 2016|[Microsoft Connectors v4.0 for Oracle and Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>下載最新的 SQL Server Data Tools (SSDT)

在此取得最新版的 SSDT：  
[下載 SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
