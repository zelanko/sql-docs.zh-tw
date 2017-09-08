---
title: "Microsoft Connectors for Oracle and Teradata by Attunity (SSIS) |Microsoft 文件"
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors for Oracle and Teradata by Attunity for Integration Services (SSIS)

您可以下載連接器 by Attunity 的 Integration services，SSIS 封裝中的資料與 Oracle 或 Teradata 載入時將效能最佳化。

## <a name="download-the-latest-attunity-connectors"></a>下載最新的 Attunity 連接器

取得最新版的連接器：  
[Microsoft Connectors for Oracle and Teradata 的 v5.0](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>問題-Attunity 連接器參數不會顯示在 SSIS 工具箱

若要查看 Attunity 連接器，在 [SSIS 工具箱] 中的，您一定要安裝的版本，目標為 SQL Server Data Tools (SSDT) 的版本相同版本的 SQL Server 安裝在電腦上的連接器。 （您也可能會有舊版安裝的連接器）。這項需求與您想要 SSIS 專案和封裝中的目標的 SQL Server 的版本無關。

例如，如果您已安裝最新版的 SSDT，您擁有 SSDT 的版本 17 標上組建編號開頭為 14。 此版本的 SSDT 新增支援 SQL Server 2017。 若要查看及使用 Attunity 連接器在 SSIS 中的封裝開發-即使您想要的目標是舊版的 SQL Server-您也必須安裝最新版的 Attunity 連接器 5.0 版。 這個版本的連接器也新增支援 SQL Server 2017。

請檢查安裝的 SSDT，從 Visual Studio 中的版本**協助** | **關於 Microsoft Visual Studio**，或在**程式和功能**在控制台中。 下表中，然後安裝 Attunity 連接器的對應版本。

|SSDT 版本|SSDT 組建編號|目標 SQL Server 版本|連接器的必要的版本|
|---------|---------|---------|---------|
|17|一開始就有 14|SQL Server 2017|[Microsoft Connectors for Oracle and Teradata 的 v5.0](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|一開始就有 13|SQL Server 2016|[Microsoft Connectors for Oracle and Teradata 的 v4.0](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>下載最新 SQL Server Data Tools (SSDT)

取得最新版的 SSDT 這裡：  
[下載 SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
