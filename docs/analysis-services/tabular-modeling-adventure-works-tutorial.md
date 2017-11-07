---
title: "表格式模型化 （Adventure Works 教學課程） |Microsoft 文件"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
keywords:
- Analysis Services
- "表格式模型"
- "教學課程"
- SSAS
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 811b5df37a88fa7a03eec2b9bc05acb87ec67bcc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/27/2017

---
# <a name="tabular-modeling-adventure-works-tutorial"></a>表格式模型化 (Adventure Works 教學課程)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

本教學課程提供有關如何建立在 Analysis Services 表格式模型的課程[1200年相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)使用[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)，並將您的模型部署到 Analysis Services伺服器內部部署或在 Azure 中。  
 
如果您使用 SQL Server 2017 或 Azure Analysis Services，而且您想要在 1400年相容性層級建立模型，請使用[Azure Analysis Services-Adventure Works 教學課程](https://review.docs.microsoft.com/azure/analysis-services/tutorials/aas-adventure-works-tutorial?branch=master)。 此更新的版本使用新的現代化取得資料 功能，連接並匯入資料來源，並使用 M 語言來設定資料分割。
 
  
## <a name="what-youll-learn"></a>學習內容   
  
-   如何在 SSDT 中建立新的表格式模型專案。
  
-   如何將資料從 SQL Server 關聯式資料庫匯入表格式模型專案。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立及管理計算、量值和關鍵效能指標，幫助使用者分析模型資料。  
  
-   如何建立及管理檢視方塊和階層，透過提供業務和應用程式專屬視點的方式幫助使用者更輕鬆地瀏覽模型。  
  
-   如何建立分割區，將資料表資料分成較小的邏輯部分，以便讓其他分割區單獨處理。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何將表格式模型部署到 Analysis Services 伺服器在內部部署或 Azure。  
  
## <a name="scenario"></a>狀況  
本教學課程根據 Adventure Works Cycles，一家虛構公司。 Adventure Works 則是大型多語系製造公司，製造及批發金屬和複合器材自行車給北美、 歐洲和亞洲。 與總公司在華盛頓 Bothell，該公司雇用 500 位員工。 此外，Adventure Works 採用數個區域銷售團隊其銷售市場所在地。  
  
為了針對銷售和行銷團隊及資深管理階層的資料分析需要提供更佳的支援，您的工作是要建立表格式模型，讓使用者分析 AdventureWorksDW 範例資料庫中的網際網路銷售資料。  
  
為了完成本教學課程及 Adventure Works Internet Sales 表格式模型，您必須完成一系列課程。 每個課程中都有一些工作，您必須依序完成每項工作才能完成課程。 在特定課程中可能有幾項工作，以達成類似的結果，但是完成每項工作的方式有些許不同。 這是為了顯示通常會有一個以上的方式來完成特定工作，並要求您使用您已在先前的工作中學到的技術。  
  
這些課程的目的是引導您完成撰寫在記憶體中模式中執行的許多功能包含在 SSDT 中使用的基本表格式模型。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。 當您完成之後的所有課程時，您將撰寫並部署 Adventure Works Internet Sales 範例表格式模型，Analysis Services 伺服器上。  
  
本教學課程並未提供下列相關課程或資訊：使用 SQL Server Management Studio 管理部署的表格式模型資料庫，或使用報表用戶端應用程式連接到部署的模型以瀏覽模型資料。  
  
## <a name="prerequisites"></a>必要條件  
若要完成本教學課程，您將需要下列必要條件：  
  
-   最新版的 [！包含[s](../ssdt/download-sql-server-data-tools-ssdt.md)。

-   SQL Server Management Studio 最新版本。 [取得最新版本](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 
  
-   用戶端應用程式，例如[Power BI Desktop](https://powerbi.microsoft.com/desktop/)或[!INCLUDE[msCoName](../includes/msconame-md.md)]Excel。    
  
-   Adventure Works DW 2014 範例資料庫與 SQL Server 執行個體。 這個範例資料庫包括完成本教學課程所需的資料。 [取得最新版本](http://go.microsoft.com/fwlink/?LinkID=335807)。  
  

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
  
  
  


