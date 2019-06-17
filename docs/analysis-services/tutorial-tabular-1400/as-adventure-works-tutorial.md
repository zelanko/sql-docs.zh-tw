---
title: Analysis Services Adventure Works Internet Sales 教學課程 (1400) |Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 39d4c0e19d89438aa08ff2f7ead24184196d5412
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503279"
---
# <a name="adventure-works-internet-sales-tutorial-1400"></a>Adventure Works Internet Sales 教學課程 (1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

本教學課程提供有關如何建立和部署的表格式模型的課程[1400年相容性層級](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。 如果您熟悉 Analysis Services 和表格式模型化時，完成本教學課程是以了解如何建立及使用 Visual Studio 中部署基本表格式模型最快的方式。 一旦具備必要條件就緒，它應該需要二至三個小時才能完成。  
  
## <a name="what-you-learn"></a>您學到什麼   
  
-   如何建立新的表格式模型專案，在**1400年相容性層級**使用 SSDT 的 Visual Studio 中。
  
-   如何將關聯式資料庫的資料匯入到表格式模型專案工作區資料庫。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立導出資料行、 量值和關鍵效能指標，幫助使用者分析重要商務計量。  
  
-   如何建立及管理檢視方塊和協助使用者更輕鬆地提供商務和應用程式專屬視點，以瀏覽模型資料的階層。  
  
-   如何建立分割區，將資料表資料分成較小的邏輯部分，以便讓其他分割區單獨處理。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何部署的表格式模型**Azure Analysis Services**伺服器或**SQL Server 2017 Analysis Services**使用 SSDT 的伺服器。  
  
## <a name="prerequisites"></a>先決條件  

若要完成本教學課程中，您需要：  
  
-   Azure Analysis Services 伺服器或在表格式模式中的 SQL Server 2017 Analysis Services 伺服器。 免費註冊[Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)並[建立伺服器](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server)或下載免費[SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。

-   [Azure SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal)具有**AdventureWorksDW 範例資料庫**，或使用內部部署 SQL Server 資料倉儲[AdventureWorksDW 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 安裝 AdventureWorksDW 資料庫到內部部署 SQL Server 資料倉儲，請使用對應的範例資料庫版本與您的伺服器版本。 

    **重要：** 如果您將範例資料庫安裝到內部部署 SQL Server 資料倉儲，並將模型部署到 Azure Analysis Services 伺服器，[內部部署資料閘道](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)需要。

-   最新版[SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。 或者，如果您已經有 Visual Studio 2017，您可以下載並安裝[Microsoft Analysis Services 專案](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)(VSIX) 封裝。 本教學課程中，SSDT 與 Visual Studio 參考的意義相同。 

-   最新版[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。    

-   用戶端應用程式，例如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。 

## <a name="scenario"></a>狀況  

本教學課程根據 Adventure Works Cycles，這家虛構公司。 Adventure Works 是大型的跨國製造公司，製造及批發自行車、 零件和配件的北美洲、 歐洲和亞洲的商業市場。 該公司雇用 500 名員工。 此外，Adventure Works 採用數個區域的銷售團隊，遍其市場規模。 您的專案為建立表格式模型，讓銷售和行銷使用者分析 AdventureWorksDW 資料庫中的網際網路銷售資料。  
  
若要完成本教學課程，您必須完成各個課程。 在每個課程中，有一些工作。 完成每個工作順序，才能完成本課程。 而在特定的課程中可能有幾項工作會達成類似的結果，但是完成每項工作的方式會稍有不同。 這個方法會顯示通常是一個以上的方式來完成工作，並激發您運用您已了解先前的課程和工作中的技術。  
  
這些課程的目的是引導您使用的許多功能包含在 SSDT 中製作基本表格式模型。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。
  
本教學課程並不會提供有關管理伺服器，以在 Azure 入口網站，使用 SSMS，或使用瀏覽模型資料的用戶端應用程式管理的伺服器或資料庫中的課程。 


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

這些課程不需要完成這個教學課程中，但是能幫助您更了解進階表格式模型撰寫功能。  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[詳細資料列](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 分鐘|
|[動態安全性](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 分鐘|
|[不完全的階層](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 分鐘| 

  
## <a name="next-steps"></a>後續步驟  

若要開始，請參閱[第 1 課：建立新的表格式模型專案](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

