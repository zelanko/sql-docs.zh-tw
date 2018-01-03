---
title: "R 和 SQL Server 的端對端資料科學逐步解說 |Microsoft 文件"
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 9d6654109e3cb5ff2e2c174dc37fd02bfc02dcb3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2017
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R 和 SQL Server 的端對端資料科學逐步解說

在本逐步解說中，您要開發 Microsoft R 與 SQL Server 2016 或 SQL Server 2017 為基礎的預測模型的端對端解決方案。

本逐步解說是根據一組常用的公用資料，即紐約市計程車資料集。 您使用的 R 程式碼中，組合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料，以及自訂的 SQL 函式來建立分類模型，表示驅動程式可能會收到提示，以在特定計程車時的機率。 您也可以部署到您的 R 模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]且使用伺服器資料來產生分數以模型為基礎。

這個範例可以擴充至所有類型的真實生活的問題，例如預測銷售的活動時，客戶回應或預測的消費或出席事件。 模型可以叫用預存程序，因為可以輕鬆地將它內嵌在應用程式。

由於導入 R 開發人員設計的逐步解說[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，盡可能使用 R。 不過，這不表示 R 一定是每一項工作的最佳工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。  這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。 我們嘗試在指出一路進行最佳化的次數。

> [!NOTE]
> 此逐步解說原先的開發對象和測試環境是 SQL Server 2016。 不過，螢幕擷取畫面和程序已更新使用 SQL Server Management Studio，這適用於 SQL Server 2017 最新版本。

## <a name="overview"></a>概觀

預估時間不包括安裝程式。 如需詳細資訊，請參閱[逐步解說的必要條件](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

|主題清單|預估時間|
|-|------------------------------|
|[準備 R 逐步解說資料](../tutorials/walkthrough-prepare-the-data.md) <br /><br />取得用於建置模型的資料。 下載公用資料集並將它載入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。|30 分鐘|
|[使用 SQL 瀏覽資料](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />了解您使用 SQL 工具和摘要的資料。|10 分鐘|
|[使用 R 摘要資料](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />使用 R 來探索資料並產生摘要。|10 分鐘|
|[建立 SQL Server 中使用 R 的繪圖](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />混合使用 R 與 SQL，在本機和遠端計算內容中建立繪圖。|10 分鐘|
|[建立使用 R 和 T-SQL 資料功能）](../tutorials/walkthrough-create-data-features.md) <br /><br />在 R 和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中使用自訂函式來執行特徵工程。 比較 R 和 T-SQL 在功能化工作方面的效能。 |10 分鐘|
|[建立 R 模型，並將它儲存在 SQL Server](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />訓練及微調預測模型。 評估模型效能。 此逐步解說會建立一個分類模型。 使用 R 來策畫模型的精確度。|15 分鐘|
|[部署使用 SQL Server R 模型](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以在生產環境中部署。 從預存程序呼叫模型以產生預測。|10 分鐘|

### <a name="intended-audience"></a>適用對象

本逐步解說適用於 R 或 SQL 開發人員。 它介紹如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 將 R 整合至企業工作流程。  您應該熟悉資料庫作業，例如建立資料庫和資料表、 匯入資料，以及執行查詢。

+ 所有 SQL 與 R 指令碼都會包含項目。
+ 您可能需要修改指令碼，在您的環境中執行中的字串。 您可以使用任何程式碼編輯器，例如[Visual Studio Code](https://code.visualstudio.com/Download)。

### <a name="prerequisites"></a>Prerequisites

+ 您必須存取的 SQL Server 2016 中，執行個體或 SQL Server 2017 評估版。
+ SQL Server 電腦上必須至少有一個執行個體已安裝 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。
+ 如果您想要從遠端電腦，例如膝上型電腦或其他網路的電腦執行 R 指令，您必須安裝 Microsoft R Open 的程式庫。 您可以安裝 Microsoft R 用戶端或 Microsoft R Server。 遠端電腦必須能夠連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。
+ 如果您需要將用戶端和伺服器放在相同電腦上，請務必傳送 R 指令碼從 「 遠端 」 的用戶端安裝一組個別的 Microsoft R 程式庫使用。 請勿使用已安裝的 R 程式庫使用 SQL Server 執行個體為此目的。

如需有關如何設定這些伺服器和用戶端環境的詳細資訊，請參閱[R 和 SQL Server 的資料科學逐步解說的必要條件](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)。

## <a name="next-lesson"></a>下一課

[準備 R 逐步解說資料](../tutorials/walkthrough-prepare-the-data.md)
