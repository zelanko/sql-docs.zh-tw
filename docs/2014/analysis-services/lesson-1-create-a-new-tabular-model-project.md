---
title: 第 1 課：建立新的表格式模型專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7ab0a864d99e3cade96b7715adf7d307ca355c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729468"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>第 1 課：建立新的表格式模型專案
  在這一課，您將在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中建立新的空白表格式模型專案。 建立新專案之後，您就可以使用 [資料表匯入精靈] 開始加入資料。 除了建立新專案之外，這一課還包括 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中表格式模型撰寫環境的簡介。  
  
 若要深入了解不同類型的表格式模型專案，請參閱[表格式模型專案 &#40;SSAS 表格式&#41;](tabular-models/tabular-model-projects-ssas-tabular.md)。 若要深入了解表格式模型撰寫環境，請參閱[表格式模型設計工具&#40;SSAS 表格式&#41;](tabular-model-designer-ssas-tabular.md)。  
  
 估計的時間才能完成這一課：**10 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型撰寫教學課程的第一課。 若要完成本課，您必須在 SQL Server 執行個體上安裝 AdventureWorksDW 資料庫。 如需詳細資訊，請參閱[表格式模型化 &#40;Adventure Works 教學課程&#41;](tabular-modeling-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>建立新的表格式模型專案  
  
#### <a name="to-create-a-new-tabular-model-project"></a>若要建立新的表格式模型專案  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]的 **[檔案]** 功能表上，按一下 **[新增]**，然後再按一下 **[專案]**。  
  
2.  在 **新的專案**對話方塊的 **已安裝的範本**，按一下  **Business Intelligence**，然後按一下  **Analysis Services**，和然後按一下**Analysis Services 表格式專案**。  
  
3.  在 **名稱**，型別`AW Internet Sales Tabular Model`，然後指定專案檔的位置。  
  
     根據預設，[方案名稱] 將與專案名稱相同，不過您可以輸入不同的方案名稱。  
  
4.  按一下 [確定] 。  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>了解 SQL Server 資料工具表格式模型撰寫環境  
 既然您已建立新的表格式模型專案，讓我們花一點時間瀏覽表格式模型撰寫環境中的[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)](Visual Studio 2010 或更新版本)。  
  
 建立專案之後，該專案會在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中開啟。 模型設計師會顯示空白模型，並選取 **方案總管** 視窗中的 **Model.bim** 檔。 當您加入資料時，資料表和資料行將出現在設計師中。 如果您未看見設計師 （含有 [Model.bim] 索引標籤的空視窗），在**方案總管**下方`AW Internet Sales Tabular Model`，按兩下**Model.bim**檔案。  
  
 您可以在 [屬性] 視窗中檢視基本專案屬性。 在 **方案總管**，按一下  `AW Internet Sales Tabular Model`。 請注意，您會在 [屬性] 視窗的 [專案檔] 中看見 **AW Internet Sales Tabular Model.smproj**。 這是專案檔的名稱，[專案資料夾] 中則會顯示專案檔的位置。  
  
 在 **方案總管**，以滑鼠右鍵按一下`AW Internet Sales Tabular Model`專案，然後再按一下**屬性**。 [AW Internet Sales Tabular Model 屬性頁] 對話方塊隨即出現。 這些是進階專案屬性。 稍後您將在準備好部署模型時，設定其中部分屬性。  
  
 現在，讓我們看看模型屬性。 在 **方案總管**中，按一下 **Model.bim**。 現在您會在 [屬性] 視窗中看見模型屬性，其中最重要的屬性是 [DirectQuery 模式] 屬性。 此屬性指定模型是以 In-Memory 模式 (關閉) 或是 DirectQuery 模式 (開啟) 部署。 在本教學課程中，您將撰寫及部署記憶體中模式的模型。  
  
 當您建立新模型時，某些模型屬性會根據可在 [工具\選項] 對話方塊中指定的 [資料模型] 設定自動設定。 [資料備份]、[工作空間保留] 和 [工作空間伺服器] 屬性會指定備份、在記憶體中保留以及建立工作空間資料庫 (您的模型撰寫資料庫) 的方式和位置。 您稍後可以視需要變更這些設定，但目前讓這些屬性保持不變。  
  
 安裝 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]之後，Visual Studio 環境中會加入幾個新的功能表項目。 讓我們看看撰寫表格式模型所特有的新功能表項目。 按一下 [模型] 功能表。 您可以從此處啟動 [資料表匯入精靈]、檢視和編輯現有的連接、重新整理工作空間資料、在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 中使用 [在 Excel 中進行分析] 功能瀏覽您的模型、建立檢視方塊和角色、選取模型檢視，以及設定計算選項。  
  
 按一下 [資料表] 功能表。 您可以在此建立及管理資料表之間的關聯性、建立和管理、指定日期資料表設定、建立分割區，以及編輯資料表屬性。  
  
 按一下 [資料行] 功能表。 您可以在此於資料表中加入和刪除資料行、凍結資料行，以及指定排序次序。 您也可以使用 [自動加總] 功能為選取的資料行建立標準彙總量值。 其他工具列按鈕可讓您快速存取常用的功能和命令。  
  
 瀏覽撰寫表格式模型之各種不同專屬功能的對話方塊和位置。 雖然某些項目還無法使用，但是您仍然可以深入認識表格式模型撰寫環境。  
  
## <a name="next-steps"></a>後續步驟  
 若要繼續本教學課程，請移至下一課：[第 2 課：將資料加入](lesson-2-add-data.md)。  
  
  
