---
title: Analysis Services Adventure Works 教學課程 (1400) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28aa401eb037fecadca17ededf041ab82a4bc498
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044572"
---
# <a name="tabular-modeling-1400-compatibility-level"></a>表格式模型化 （1400年相容性層級）

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

本教學課程提供如何建立及部署表格式模型在課程[1400年相容性層級](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。 如果您還不熟悉 Analysis Services 和表格式模型化，完成本教學課程是以了解如何建立及使用 Visual Studio 部署的基本表格式模型最快的方式。 一旦您擁有必要條件就地，它應該需要兩到三小時才能完成。  
  
## <a name="what-you-learn"></a>您了解的內容   
  
-   如何建立新的表格式模型專案，在**1400年相容性層級**Visual Studio 中使用 SSDT。
  
-   如何從關聯式資料庫匯入資料到表格式模型專案的工作空間資料庫。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立導出資料行、 量值和關鍵效能指標，幫助使用者分析重要商務標準。  
  
-   如何建立及管理檢視方塊和幫助使用者更輕鬆地瀏覽模型資料，藉由提供業務和應用程式特有視點的階層。  
  
-   如何建立分割區，將資料表資料分成較小的邏輯部分，以便讓其他分割區單獨處理。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何部署表格式模型**Azure Analysis Services**伺服器或**SQL Server 2017 Analysis Services**使用 SSDT 的伺服器。  
  
## <a name="prerequisites"></a>필수 구성 요소  

若要完成本教學課程，您需要：  
  
-   Azure Analysis Services 伺服器或在表格式模式中的 SQL Server 2017 Analysis Services 伺服器。 註冊免費的[Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)和[建立伺服器](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server)或下載免費[SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

-   [Azure SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal)與**AdventureWorksDW 範例資料庫**，或具有內部部署 SQL Server 資料倉儲[AdventureWorksDW 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 安裝時 AdventureWorksDW 資料庫到在內部部署 SQL Server 資料倉儲，使用對應的範例資料庫版本與伺服器版本。 

    **重要事項：** 如果您在內部部署 SQL Server 資料倉儲，安裝範例資料庫，並將您的模型部署到 Azure Analysis Services 伺服器，[在內部部署資料閘道](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)需要。

-   最新版[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 或者，如果您已經有 Visual Studio 2017，您可以下載並安裝[Microsoft Analysis Services 專案](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)(功能 VSIX) 封裝。 此教學課程中，參考 SSDT 和 Visual Studio 的意義相同。 

-   最新版[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。    

-   用戶端應用程式，例如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。 

## <a name="scenario"></a>狀況  

本教學課程根據 Adventure Works Cycles，一家虛構公司。 Adventure Works 則是大型的跨國製造公司，製造及批發自行車、 parts 和附屬應用程式在北美、 歐洲和亞洲的商業市場。 該公司雇用 500 位員工。 此外，Adventure Works 採用數個區域銷售團隊其銷售市場所在地。 若要建立表格式模型，讓銷售及行銷使用者分析 AdventureWorksDW 資料庫中的網際網路銷售資料是您的專案。  
  
若要完成本教學課程，您必須完成各種課程。 在每個課程中，有的工作。 完成每項工作順序才能完成課程。 在特定課程中可能有幾項工作，以達成類似的結果，但是完成每項工作的方式有些許不同。 這個方法會顯示通常是一個以上的方式來完成工作，並要求您使用您學到先前的課程和工作中的技術。  
  
這些課程的目的是引導您完成基本的表格式模型撰寫使用許多 SSDT 中包含的功能。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。
  
本教學課程不會提供有關管理伺服器，以在 Azure 入口網站，使用 SSMS，或使用瀏覽模型資料的用戶端應用程式管理的伺服器或資料庫中的課程。 


## <a name="lessons"></a>課程  

這個教學課程包括下列課程：  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[1-建立新的表格式模型專案](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 分鐘|  
|[2 - 取得資料](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 分鐘|  
|[3 - 標記為日期資料表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 分鐘|  
|[4 - 建立關聯性](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 分鐘|  
|[5 - 建立導出資料行](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 分鐘|
|[6 - 建立量值](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 分鐘|  
|[7-建立關鍵效能指標 (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 分鐘|  
|[8 - 建立檢視方塊](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 分鐘|  
|[9 - 建立階層](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 分鐘|  
|[10 - 建立分割區](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 分鐘|  
|[11 - 建立角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 分鐘|  
|[12 - 在 Excel 中進行分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 分鐘| 
|[13 - 部署](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 分鐘|  
  
## <a name="supplemental-lessons"></a>補充課程  

這些課程不需要完成這個教學課程中，但可能有助於更佳了解進階表格式模型撰寫功能。  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[詳細資料列](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 分鐘|
|[動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 分鐘|
|[不完全的階層](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 分鐘| 

  
## <a name="next-steps"></a>後續的步驟  

若要開始使用，請參閱[第 1 課： 建立新的表格式模型專案](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

