---
title: 多維度模型化 （Adventure Works 教學課程） |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98e995a89f9993a54736c4966639fd583e2391b6
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403720"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>多維度模型化 (Adventure Works 教學課程)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

歡迎使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 教學課程。 這個教學課程描述如何使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 來開發和部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，所有範例都使用虛構公司 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 。  
  
## <a name="what-you-learn"></a>您學到什麼  
在本教學課程中，您將學會下列作業：  
  
-   如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]專案中定義資料來源、資料來源檢視、維度、屬性、屬性關聯性、階層和 Cube。  
  
-   如何透過將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體，檢視 Cube 和維度資料，以及如何處理已部署的物件，以便使用基礎資料來源中的資料擴展這些物件。  
  
-   如何在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中修改量值、維度、階層、屬性和量值群組，以及如何將累加變更部署到開發伺服器上已部署的 Cube。  
  
-   如何在 Cube 內定義計算、關鍵效能指標 (KPI)、動作、檢視方塊、翻譯和安全性角色。  
  
案例描述隨附此教學課程，讓您可以更了解這些課程的內容。 如需詳細資訊，請參閱＜ [Analysis Services Tutorial Scenario](analysis-services-tutorial-scenario.md)＞。  
  
## <a name="prerequisites"></a>先決條件  
若要完成這個教學課程的所有課程，您將需要範例資料、範例專案檔及軟體。 如需如何尋找及安裝這個教學課程之必要條件的指示，請參閱＜ [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](install-sample-data-and-projects.md)＞。  
  
另外還要具備下列權限才能順利完成這個教學課程：  
  
-   您必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 電腦上 Administrators 本機群組的成員，或是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體中伺服器管理角色的成員。  
  
-   您必須擁有讀取權限**AdventureWorksDW**範例資料庫。 這個範例資料庫對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本有效。  
  
## <a name="lessons"></a>課程  
這個教學課程包括下列課程。  
  
|課程|估計完成時間|  
|----------|------------------------------|  
|[第 1 課：定義資料來源檢視中的 Analysis Services 專案](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 分鐘|  
|[第 2 課：定義和部署 Cube](lesson-2-defining-and-deploying-a-cube.md)|30 分鐘|  
|[第 3 課：修改量值、 屬性和階層](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 分鐘|  
|[第 4 課：定義進階的屬性和維度屬性](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 分鐘|  
|[第 5 課：定義維度和量值群組之間的關聯性](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 分鐘|  
|[第 6 課：定義計算](lesson-6-defining-calculations.md)|45 分鐘|  
|[第 7 課：定義關鍵效能指標&#40;Kpi&#41;](lesson-7-defining-key-performance-indicators-kpis.md)|30 分鐘|  
|[第 8 課：定義動作](lesson-8-defining-actions.md)|30 分鐘|  
|[第 9 課：定義檢視方塊和翻譯](lesson-9-defining-perspectives-and-translations.md)|30 分鐘|  
|[第 10 課：定義系統管理角色](lesson-10-defining-administrative-roles.md)|15 分鐘|  
  
> [!NOTE]  
> 您將在本教學課程中建立的 cube 資料庫是一個簡化的版的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]屬於可供下載 GitHub 上的 Adventure Works 範例資料庫的多維度模型專案。 Adventure Works 多維度資料庫的教學課程版本經過簡化，更著重在您想要立即熟練的特定技巧上。 完成此教學課程之後，請考慮自行瀏覽多維度模型專案，以更了解 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度模型。  
  
## <a name="next-step"></a>下一個步驟  
若要開始本教學課程，請繼續進行第 1 課：[第 1 課：定義資料來源檢視中的 Analysis Services 專案](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)。  
  
  
  
