---
title: Analysis Services Internet Sales 教學課程 （1200年相容性層級） |Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b3aace2320882d209e6a7ab0f67a16a6f8a6df
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503624"
---
# <a name="adventure-works-internet-sales-tutorial-1200"></a>教學課程中 adventure Works Internet Sales (1200)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

本教學課程提供有關如何建立在 Analysis Services 表格式模型的課程[1200年相容性層級](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)利用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)，並將模型部署到 Analysis Services伺服器在內部部署或 Azure 中。  
 
如果您使用 SQL Server 2017 或 Azure Analysis Services，而且您想要建立您的模型在 1400年相容性層級，請使用[表格式模型 （1400年相容性層級）](../tutorial-tabular-1400/as-adventure-works-tutorial.md)。 此更新的版本會使用新式 Get Data 功能連接並匯入來源資料、 使用 M 語言來設定資料分割，並包含其他補充課程。

> [!IMPORTANT]
> 您應該建立您的表格式模型，您的伺服器所支援的最新相容性層級。 更新版本的相容性層級模型提供改進的效能，額外的功能，並將更順暢地升級至未來的相容性層級。
 
  
## <a name="what-you-learn"></a>您學到什麼   
  
-   如何在 SSDT 中建立新的表格式模型專案。
  
-   如何將資料從 SQL Server 關聯式資料庫匯入表格式模型專案。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立及管理計算、量值和關鍵效能指標，幫助使用者分析模型資料。  
  
-   如何建立及管理檢視方塊和協助使用者更輕鬆地提供商務和應用程式專屬視點，以瀏覽模型資料的階層。  
  
-   如何建立從其他分割區的獨立資料分割將資料表資料分割成較小的邏輯部分，可處理。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何以 Analysis Services 伺服器在內部部署或 Azure 中部署表格式模型。  
  
## <a name="scenario"></a>狀況  
本教學課程根據 Adventure Works Cycles，這家虛構公司。 Adventure Works 是大型的跨國製造公司產生自行車、 零件和配件的北美洲、 歐洲和亞洲的商業市場。 總公司在華盛頓 Bothell，該公司雇用 500 名員工。 此外，Adventure Works 採用數個區域的銷售團隊，遍其市場規模。  
  
為了針對銷售和行銷團隊及資深管理階層的資料分析需要提供更佳的支援，您的工作是要建立表格式模型，讓使用者分析 AdventureWorksDW 範例資料庫中的網際網路銷售資料。  
  
為了完成本教學課程及 Adventure Works Internet Sales 表格式模型，您必須完成一系列課程。 在每一課是許多工作;完成每個工作順序，才能完成本課程。 而在特定的課程中可能有幾項工作會達成類似的結果，但是完成每項工作的方式會稍有不同。 這是要說明通常會有一個以上的方式來完成特定工作，並激發您運用先前工作中學習的技術。  
  
這些課程的目的是引導您製作基本表格式模型使用的許多功能在 SSDT 中包含在記憶體中模式中執行。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。 當您完成之後的所有課程時，您已撰寫，並部署 Adventure Works Internet Sales 範例表格式模型，Analysis Services 伺服器上。  
  
本教學課程並未提供下列相關課程或資訊：使用 SQL Server Management Studio 管理部署的表格式模型資料庫，或使用報表用戶端應用程式連接到部署的模型以瀏覽模型資料。  
  
## <a name="prerequisites"></a>先決條件  
若要完成本教學課程中，您需要下列必要條件：  
  
-   最新版[SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)。

-   SQL Server Management Studio 的最新版本。 [取得最新版本](../../ssms/download-sql-server-management-studio-ssms.md)。 
  
-   用戶端應用程式，例如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。    
  
-   Adventure Works DW 範例資料庫與 SQL Server 執行個體。 這個範例資料庫包括完成本教學課程所需的資料。 [取得最新版本](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。  
  

-   Azure Analysis Services 或 SQL Server 2016 或更新版本的 Analysis Services 執行個體來部署您的模型。 [註冊免費的 Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)。
  
## <a name="lessons"></a>課程  
這個教學課程包括下列課程：  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[第 1 課：建立新的表格式模型專案](lesson-1-create-a-new-tabular-model-project.md)|10 分鐘|  
|[第 2 課：加入資料](lesson-2-add-data.md)|20 分鐘|  
|[第 3 課：標記為日期資料表](lesson-3-mark-as-date-table.md)|3 分鐘|  
|[第 4 課：建立關聯性](lesson-4-create-relationships.md)|10 分鐘|  
|[第 5 課：建立導出資料行](lesson-5-create-calculated-columns.md)|15 分鐘|
|[第 6 課：建立量值](lesson-6-create-measures.md)|30 分鐘|  
|[第 7 課：建立關鍵效能指標](lesson-7-create-key-performance-indicators.md)|15 分鐘|  
|[第 8 課：建立檢視方塊](lesson-8-create-perspectives.md)|5 分鐘|  
|[第 9 課：建立階層](lesson-9-create-hierarchies.md)|20 分鐘|  
|[第 10 課：建立資料分割](lesson-10-create-partitions.md)|15 分鐘|  
|[第 11 課：建立角色](lesson-11-create-roles.md)|15 分鐘|  
|[第 12 課：在 Excel 中進行分析](lesson-12-analyze-in-excel.md)|20 分鐘| 
|[第 13 課：部署](lesson-13-deploy.md)|5 分鐘|  
  
## <a name="supplemental-lessons"></a>補充課程  
本教學課程也包含補充課程。 本節中的主題並非完成教學課程所必須，但是能幫助您更了解進階表格式模型撰寫功能。  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[使用資料列篩選器實作動態安全性](supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 分鐘|  
|[設定 Power View 報表的報表屬性](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)|30 分鐘| 

  
## <a name="next-steps"></a>後續步驟  
若要開始本教學課程，請繼續進行第 1 課：[第 1 課：建立新的表格式模型專案](lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

