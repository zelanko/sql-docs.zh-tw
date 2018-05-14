---
title: 表格式模型 （1200年相容性層級） |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b0b8d60c6c365d48f8eccc46cbc9a3b0f5222ff5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="tabular-modeling-1200-compatibility-level"></a>表格式模型化 （1200年相容性層級）
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

本教學課程提供有關如何建立在 Analysis Services 表格式模型的課程[1200年相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)使用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)，並將您的模型部署到 Analysis Services伺服器內部部署或在 Azure 中。  
 
如果您使用 SQL Server 2017 或 Azure Analysis Services，而且您想要在 1400年相容性層級建立模型，請使用[表格式模型 （1400年相容性層級）](tutorial-tabular-1400/as-adventure-works-tutorial.md)。 此更新的版本使用現代的取得資料 功能來連接並匯入來源資料，會使用的 M 語言來設定資料分割，並包含額外補充課程。

> [!IMPORTANT]
> 您應該建立您的表格式模型，您的伺服器支援的最新相容性層級。 更新的相容性層級模型提供改進的效能，額外的功能，並將會更順暢地升級至未來的相容性層級。
 
  
## <a name="what-you-learn"></a>您了解的內容   
  
-   如何在 SSDT 中建立新的表格式模型專案。
  
-   如何將資料從 SQL Server 關聯式資料庫匯入表格式模型專案。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立及管理計算、量值和關鍵效能指標，幫助使用者分析模型資料。  
  
-   如何建立及管理檢視方塊和幫助使用者更輕鬆地瀏覽模型資料，藉由提供業務和應用程式特有視點的階層。  
  
-   如何建立從其他資料分割的獨立資料表資料分割成較小的邏輯部分，可以處理的資料分割。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何將表格式模型部署到 Analysis Services 伺服器在內部部署或 Azure。  
  
## <a name="scenario"></a>狀況  
本教學課程根據 Adventure Works Cycles，一家虛構公司。 Adventure Works 是大型的跨國製造公司，產生自行車、 parts 和附屬應用程式在北美、 歐洲和亞洲的商業市場。 與總公司在華盛頓 Bothell，該公司雇用 500 位員工。 此外，Adventure Works 採用數個區域銷售團隊其銷售市場所在地。  
  
為了針對銷售和行銷團隊及資深管理階層的資料分析需要提供更佳的支援，您的工作是要建立表格式模型，讓使用者分析 AdventureWorksDW 範例資料庫中的網際網路銷售資料。  
  
為了完成本教學課程及 Adventure Works Internet Sales 表格式模型，您必須完成一系列課程。 在每一課是幾項工作。完成每項工作順序才能完成課程。 在特定課程中可能有幾項工作，以達成類似的結果，但是完成每項工作的方式有些許不同。 這是為了顯示通常會有一個以上的方式來完成特定工作，並要求您使用您已在先前的工作中學到的技術。  
  
這些課程的目的是引導您完成撰寫在記憶體中模式中執行的許多功能包含在 SSDT 中使用的基本表格式模型。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。 當您完成之後的所有課程時，您所撰寫並部署 Adventure Works Internet Sales 範例表格式模型，Analysis Services 伺服器上。  
  
本教學課程並未提供下列相關課程或資訊：使用 SQL Server Management Studio 管理部署的表格式模型資料庫，或使用報表用戶端應用程式連接到部署的模型以瀏覽模型資料。  
  
## <a name="prerequisites"></a>필수 구성 요소  
若要完成本教學課程，您需要下列必要條件：  
  
-   最新版[SSDT](../ssdt/download-sql-server-data-tools-ssdt.md)。

-   SQL Server Management Studio 最新版本。 [取得最新版本](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 
  
-   用戶端應用程式，例如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或 Excel。    
  
-   Adventure Works DW 範例資料庫與 SQL Server 執行個體。 這個範例資料庫包括完成本教學課程所需的資料。 [取得最新版本](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。  
  

-   Azure Analysis Services 或 SQL Server 2016 或更新版本的 Analysis Services 執行個體部署至您的模型。 [申請免費的 Azure Analysis Services 試用版](https://azure.microsoft.com/services/analysis-services/)。
  
## <a name="lessons"></a>課程  
這個教學課程包括下列課程：  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[第 1 課：建立新的表格式模型專案](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 分鐘|  
|[第 2 課：加入資料](../analysis-services/lesson-2-add-data.md)|20 分鐘|  
|[課程 3：標記為日期資料表](../analysis-services/lesson-3-mark-as-date-table.md)|3 分鐘|  
|[第 4 課： 建立關聯性](../analysis-services/lesson-4-create-relationships.md)|10 分鐘|  
|[第 5 課： 建立導出資料行](../analysis-services/lesson-5-create-calculated-columns.md)|15 分鐘|
|[第 6 課： 建立量值](../analysis-services/lesson-6-create-measures.md)|30 分鐘|  
|[課程 7：建立關鍵效能指標](../analysis-services/lesson-7-create-key-performance-indicators.md)|15 分鐘|  
|[第 8 課： 建立檢視方塊](../analysis-services/lesson-8-create-perspectives.md)|5 分鐘|  
|[第 9 課： 建立階層](../analysis-services/lesson-9-create-hierarchies.md)|20 分鐘|  
|[第 10 課： 建立資料分割](../analysis-services/lesson-10-create-partitions.md)|15 分鐘|  
|[第 11 課： 建立角色](../analysis-services/lesson-11-create-roles.md)|15 分鐘|  
|[課程 12：在 Excel 中分析](../analysis-services/lesson-12-analyze-in-excel.md)|20 分鐘| 
|[課程 13：部署](../analysis-services/lesson-13-deploy.md)|5 分鐘|  
  
## <a name="supplemental-lessons"></a>補充課程  
本教學課程也包含 [補充課程](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e)。 本節中的主題並非完成教學課程所必須，但是能幫助您更了解進階表格式模型撰寫功能。  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[使用資料列篩選器實作動態安全性](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 分鐘|  

  
## <a name="next-step"></a>下一步  
若要開始本教學課程，請繼續進行第一課： [第 1 課：建立新的表格式模型專案](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
  
  

