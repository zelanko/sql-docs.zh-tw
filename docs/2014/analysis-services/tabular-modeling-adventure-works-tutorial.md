---
title: 表格式模型化 （Adventure Works 教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2693bd51da682e9af0133c8400f2cfeacd2737ca
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53373680"
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>表格式模型化 (Adventure Works 教學課程)
  本教學課程提供如何使用 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 建立 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Analysis Services 表格式模型的課程。  
  
## <a name="what-you-will-learn"></a>學習內容  
 在這個教學課程進行期間，您將學習下列內容：  
  
-   如何在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中建立新的表格式模型專案。  
  
-   如何將資料從 SQL Server 關聯式資料庫匯入表格式模型專案。  
  
-   如何在模型中建立及管理資料表之間的關聯性。  
  
-   如何建立及管理計算、量值和關鍵效能指標，幫助使用者分析模型資料。  
  
-   如何建立及管理檢視方塊和階層，透過提供業務和應用程式專屬視點的方式幫助使用者更輕鬆地瀏覽模型。  
  
-   如何建立分割區，將資料表資料分成較小的邏輯部分，以便讓其他分割區單獨處理。  
  
-   如何透過為使用者成員建立角色的方式保護模型物件和資料的安全。  
  
-   如何將表格式模型部署到以表格式模式執行之 Analysis Services 的沙箱或實際執行個體中。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 這個教學課程是以一家虛構的公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]為基礎。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司，專門生產及批發金屬和合成器材自行車給北美、歐洲和亞洲的商場。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的總公司在華盛頓 Bothell，該公司雇用 500 位員工。 另外，[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 它的市場還雇用了一些地區銷售團隊。  
  
 為了針對銷售和行銷團隊及資深管理階層的資料分析需要提供更佳的支援，您的工作是要建立表格式模型，讓使用者分析 AdventureWorksDW 範例資料庫中的網際網路銷售資料。  
  
 為了完成本教學課程及 Adventure Works Internet Sales 表格式模型，您必須完成一系列課程。 每個課程中都有一些工作，您必須依序完成每項工作才能完成課程。 雖然在特定課程中可能有幾項工作會得到類似的結果，但是完成每項工作的方式會稍有不同。 主要目的在於說明通常會有多種方式可完成特定工作，並且要求您使用在之前的工作中學到的技巧。  
  
 這些課程的目的是引導您藉由使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的許多功能，來撰寫執行記憶體中模式的基本表格式模型。 因為每一課都是以上一課為基礎，所以您應該依序完成課程。 完成所有課程之後，您就已撰寫並且將 Adventure Works Internet Sales 範例表格式模型部署到 Analysis Services 伺服器上。  
  
> [!NOTE]  
>  本教學課程並未提供下列相關課程或資訊：使用 SQL Server Management Studio 管理部署的表格式模型資料庫，或使用報表用戶端應用程式連接到部署的模型以瀏覽模型資料。  
  
## <a name="prerequisites"></a>先決條件  
 您必須安裝下列必要條件，才能完成本教學課程：  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services 執行個體 (以表格式模式執行)。  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   AdventureWorksDW 範例資料庫。 這個範例資料庫包括完成本教學課程所需的資料。 若要下載範例資料庫，請參閱[ https://go.microsoft.com/fwlink/?LinkID=335807 ](https://go.microsoft.com/fwlink/?LinkID=335807)。  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 或更新版本 (與第 11 課中的 [在 Excel 中進行分析] 功能搭配使用)  
  
## <a name="lessons"></a>課程  
 這個教學課程包括下列課程：  
  
|課程|估計完成時間|  
|------------|--------------------------------|  
|[第 1 課：建立新的表格式模型專案](lesson-1-create-a-new-tabular-model-project.md)|10 分鐘|  
|[第 2 課：加入資料](lesson-2-add-data.md)|20 分鐘|  
|[第 3 課：重新命名資料行](rename-columns.md)|20 分鐘|  
|[第 4 課：標記為日期資料表](lesson-3-mark-as-date-table.md)|3 分鐘|  
|[第 5 課：建立關聯性](lesson-4-create-relationships.md)|10 分鐘|  
|[第 6 課：建立導出資料行](lesson-5-create-calculated-columns.md)|15 分鐘|  
|[第 7 課：建立量值](lesson-6-create-measures.md)|30 分鐘|  
|[第 8 課：建立關鍵效能指標](lesson-7-create-key-performance-indicators.md)|15 分鐘|  
|[第 9 課：建立檢視方塊](lesson-8-create-perspectives.md)|5 分鐘|  
|[第 10 課：建立階層](lesson-9-create-hierarchies.md)|20 分鐘|  
|[第 11 課：建立資料分割](lesson-10-create-partitions.md)|15 分鐘|  
|[第 12 課：建立角色](lesson-11-create-roles.md)|15 分鐘|  
|[第 13 課：在 Excel 中進行分析](lesson-12-analyze-in-excel.md)|20 分鐘|  
|[第 14 課：部署](lesson-13-deploy.md)|5 分鐘|  
  
## <a name="supplemental-lessons"></a>補充課程  
 本教學課程也包含 [補充課程](../tutorials/supplemental-lessons.md)。 本節中的主題並非完成教學課程所必須，但是能幫助您更了解進階表格式模型撰寫功能。  
  
 這個教學課程包括下列補充課程：  
  
|課程|估計完成時間|  
|------------|--------------------------------|  
|[使用資料列篩選器實作動態安全性](../tutorials/implement-dynamic-security-by-using-row-filters.md)|30 分鐘|  
|[設定 Power View 報表的報表屬性](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)設定 Power View 報表的報表屬性|30 分鐘|  
  
## <a name="next-step"></a>下一個步驟  
 若要開始教學課程，請繼續進行第一課：[第 1 課：建立新的表格式模型專案](lesson-1-create-a-new-tabular-model-project.md)。  
  
  
