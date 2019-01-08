---
title: 使用 R-SQL Server Machine Learning 服務建立商業智慧 (BI) 工作流程
description: 結合商務智慧 (BI) 與 R 語言的整合案例支援 SQL Server 和 SQL Server Integration Services (SSIS) 中。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432731"
---
# <a name="creating-bi-workflows-with-r"></a>使用 R 建立 BI 工作流程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

關聯式資料庫是高度最佳化的技術，適用於提供可調整的方案，以進行交易處理、儲存及資料查詢。

相反地，傳統 R 方案一般被倚賴從各種來源，通常採用 CSV 格式，以執行進一步的資料探索和模型匯入資料。 這種作法不僅沒有效率，而且也不安全。

這篇文章描述 R 與避免常見的錯誤和安全性風險，如果資料庫外部的開發機器學習解決方案可能會發生的 SQL Server 的整合案例。

它也會描述商業智慧應用程式，尤其是 Integration Services 和 Reporting Services，如何使用 R 程式碼互動和取用資料或 r 所產生的圖形的範例

適用於：SQL Server 2016 R Services、 SQL Server 2017 Machine Learning 服務

## <a name="bring-compute-power-to-the-data"></a>為資料帶入計算能力

Machine learning 與 SQL Server 整合的主要設計目標是要讓分析貼近資料。 這會提供多項優點：

+ 資料安全性。 接近 R 帶入的資料來源，可避免浪費資源或不安全的資料移動。

+ 速度。 資料庫已針對集合型操作進行最佳化。 最新的創新，例如記憶體中資料表的資料庫中進行摘要和彙總作業如閃電般，而且與資料科學完美互補。

+ 簡化部署和整合。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是許多其他資料管理工作和應用程式的作業中心點。 使用位於報表倉儲的資料庫中的資料，您可以確定機器學習服務解決方案所使用的資料是一致且最新狀態。 

+ 跨雲端和內部部署的效率。 您可以倚賴企業資料管線 (包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure Data Factory)，而不以 R 處理資料。 透過 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 很容易就能報告結果或分析。

資料科學家和開發人員可以使用正確的 SQL 和 R 組合，來進行不同的資料處理和分析工作，因此更有效率。

## <a name="use-integration-services-for-data-transformation-and-automation"></a>使用 Integration Services，資料轉換和自動化

資料科學工作流程的互動性很高，並涉及許多資料的轉換，包括縮放、彙總、機率計算，以及重新命名與合併屬性。 資料科學家已習慣以 R、Python 或其他語言執行許多這些工作；不過，在企業資料上執行這類工作流程需要與 ETL 工具和程序的緊密整合。

由於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可讓您透過 Transact-SQL 和預存程序在 R 中執行複雜的作業，因此您連最小程度的重新開發工作都不需要，就能將 R 特定的工作與現有的 ETL 程序整合。 而是在 R 中執行需要大量記憶體的工作鏈結，資料準備可最佳化使用最有效率的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是如何自動化您的資料處理的一些概念，以及使用的模型管線[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]工作，以在 SQL database 中建立必要的資料特徵
+ 使用條件式分支切換 R 工作的計算內容
+ 執行 R 作業，在資料庫中，產生自己的資料，並與應用程式共用該資料
+ 當使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，載入儲存在文字變數中的 R 指令碼，並在 SQL Server 中執行

### <a name="examples"></a>範例

[使用 SQL Server 2016 SSIS 和 R Services 來讓您的機器學習服務能夠運作 (英文)](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

此部落格文章會示範基本的技巧，以操作 R 程式碼使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ 呼叫 R 來產生資料，並將它儲存到使用 「 執行 SQL 」 工作， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ 使用預存程序來訓練 R 模型，並將它儲存在資料庫中

+ 使用「指令碼工作」和「執行 SQL 工作」在模型上執行評分

##  <a name="bkmk_ssrs"></a> 使用 Reporting Services 視覺效果

雖然 R 可以建立圖表和有趣的視覺效果，但它與外部資料來源的整合度並不高，這表示您必須個別產生每個圖表或圖形。 此外，可能也很難進行共用。

使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，您便可以透過各種企業報告工具 (包括 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 Power BI) 都能輕鬆取用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，在 R 中執行複雜的作業。

+ 將使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]從 R 指令碼傳回的圖形物件視覺化
+ 使用 Power BI 中的資料表

### <a name="examples"></a>範例

[R Graphics Device for Microsoft Reporting Services (SSRS) (英文)](https://rgraphicsdevice.codeplex.com/)

這個 CodePlex 專案提供程式碼，可協助您建立自訂報表項目，以將 R 的圖形輸出轉譯成可在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表中使用的影像。  透過使用自訂報表項目，您可以：

+ 將使用 R Graphics Device 建立的圖表和繪圖發佈到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 儀表板

+ 將 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 參數傳遞給 R 繪圖

> [!NOTE]
> 此範例中，必須在 Reporting Services 伺服器上，以及在 Visual Studio 中安裝支援 R Graphics Device for Reporting Services 的程式碼。 此外，還需要手動編譯和設定。
