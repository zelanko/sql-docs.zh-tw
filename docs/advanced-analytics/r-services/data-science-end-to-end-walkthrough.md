---
title: "資料科學端對端逐步解說 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 資料科學端對端逐步解說
在本逐步解說中，您將使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]開發預測性模型化所使用的端對端方案。  
  
本逐步解說根據已知公用資料集 (紐約市計程車資料集)。 您將組合使用 R 程式碼、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料和自訂 SQL 函數來建立分類模型，以表示計程車司機在特定車程時獲得小費的機率。 您也會將 R 模型部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並使用伺服器資料以根據模型來產生分數。  
  
此範例可以輕鬆地擴充至所有類型的實際問題，例如預測銷售活動的客戶回應，或預測訪客對事件的花費。 因為可以從預存程序叫用模型，所以您也可以輕鬆地將它內嵌在應用程式中。  
  
**適用對象**  
  
本逐步解說適用於 R 開發人員。 您應該熟悉基本資料庫作業，例如建立資料庫、建立資料表、將資料匯入至資料表，以及使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來查詢資料表。  將會提供 SQL 和 R 指令碼，以供您執行。  
  
如果您不熟悉 R，但很了解資料庫，則本教學課程介紹如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]將 R 整合至企業工作流程。 不需要進行任何 R 編碼；會提供所有指令碼。 您需要已安裝某種類型的 R IDE，才能執行命令。  
  
**必要條件**  
  
若要執行本教學課程，您必須能夠存取已安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 執行個體。 在您的本機環境中，準備可連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資料科學工作站，然後安裝所需的 R 程式庫。  
  
如需詳細資訊，請參閱[資料科學逐步解說的必要條件 &#40;SQL Server R 服務&#41;](../../advanced-analytics/r-services/prerequisites-for-data-science-walkthroughs-sql-server-r-services.md)。  
  
## <a name="overview"></a>概觀  
本逐步解說說明進行進階分析的典型端對端方案。 您需要依序完成課程。  
  
||估計完成時間|  
|-|------------------------------|  
|[第 1 課︰準備資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)<br /><br />分析程序是從取得用於建立模型的資料開始。 您將下載公用資料集，並且將它儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。|30 分鐘|  
|[第 2 課︰檢視和瀏覽資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-2-view-and-explore-the-data-data-science-end-to-end-walkthrough.md)<br /><br />資料科學家通常會花費相當長的時間來探索資料並準備資料以進行模型化、建立新的功能，或視需要轉換資料。  您將使用 SQL 和 R 來探索資料並產生摘要。|20 分鐘|  
|[第 3 課︰建立資料特徵 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)<br /><br />您將使用 R 和 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的自訂函數來建立新的資料功能。|10 分鐘|  
|[第 4 課︰建立和儲存模型 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)<br /><br />準備好資料時，資料科學家會透過評估效能以及嘗試不同的參數，來定型並微調模型。 在本逐步解說中，您將建立分類模型，並使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料來產生預測。 您也會使用 R 來繪製模型的精確度。|15 分鐘|  
|[第 5 課︰部署和使用模型 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)<br /><br />最後，您將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，以在生產環境中部署模型，然後從預存程序呼叫模型來產生預測。|10 分鐘|  
  
## <a name="notes"></a>注意  
因為本逐步解說設計為向 R 開發人員介紹 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，所以大部分的動作都是使用 R 所完成。但這不表示 R 一定是每個工作的最佳工具。 在許多情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以提供較佳效能，尤其是資料彙總和功能工程這類工作。 這類工作特別受益於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的新功能 (例如記憶體最佳化資料行存放區索引 )。  
  
## <a name="next-step"></a>下一個步驟  
[第 1 課︰準備資料 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
