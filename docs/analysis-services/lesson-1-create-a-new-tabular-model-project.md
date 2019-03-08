---
title: 第 1 課：建立新的表格式模型專案 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 988a091fa7d536386cadd2ed3412213a2e608564
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579428"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>第 1 課：建立新的表格式模型專案
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中建立新的空白表格式模型專案。 建立新專案之後，您就可以使用 [資料表匯入精靈] 開始加入資料。 這一課也可讓您撰寫環境，在 SSDT 中的表格式模型的簡介。  
  
完成本課程的估計時間：**10 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
本主題是表格式模型撰寫教學課程的第一課。 若要完成這一課，您必須使用 SQL Server 執行個體上安裝 AdventureWorksDW 範例資料庫。 若要進一步了解，請參閱[表格式模型化&#40;Adventure Works 教學課程&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md)。  
  
## <a name="create-a-new-tabular-model-project"></a>建立新的表格式模型專案  
  
#### <a name="to-create-a-new-tabular-model-project"></a>若要建立新的表格式模型專案  
  
1.  在 SSDT 中，在**檔案**功能表上，按一下**新增** > **專案**。  
  
2.  在 **新的專案**對話方塊方塊中，展開**已安裝** > **Business Intelligence** > **Analysis Services**，然後按一下**Analysis Services 表格式專案**。  
  
3.  在 **名稱**，型別**AW 網際網路銷售**，然後指定專案檔案的位置。  
  
    根據預設，[方案名稱] 將與專案名稱相同，不過您可以輸入不同的方案名稱。  
  
4.  按一下 [確定] 。  
  
5.  在 **表格式模型設計師**對話方塊中，選取**整合式工作區**。  
  
    工作區會裝載與專案同名的表格式模型資料庫，在模型製作期間。 整合式的工作區意味著 SSDT 將會使用內建的執行個體，不需要安裝個別的 Analysis Services 伺服器執行個體，只為了撰寫模型。 若要進一步了解，請參閱[工作區資料庫](../analysis-services/tabular-models/workspace-database-ssas-tabular.md)。
      
6.  在 [相容性層級] 中，確認已選取 [SQL Server 2016 (1200)]，然後按一下 [確定]。   
 
    ![as-tabular-lesson1-tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    如果您沒有看到 SQL Server 2016 RTM (1200) 的相容性層級的清單方塊中，您不使用最新版的 SQL Server Data Tools。 若要取得最新版本，請參閱 [安裝 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)。  

    如果您使用最新版的 SSDT，您也可以選擇 SQL Server 2017 (1400)。 不過，為了完整第 13 課：部署，您必須將部署到 SQL Server 2017 或 Azure 伺服器。
      
    只建議選取較早的相容性層級，如果您想要將您已完成的表格式模型部署到執行舊版的 SQL Server 的不同 Analysis Services 執行個體。 舊版的相容性層級不支援整合式工作區。 若要深入了解，請參閱 [相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)。   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>了解 SSDT 表格式模型撰寫環境  
既然您已建立新的表格式模型專案，讓我們花一點時間瀏覽表格式模型撰寫在 SSDT 中的環境。  
  
您的專案建立之後，它會在 SSDT 中開啟。 在右側中，在**表格式模型總管**，您會看到樹狀檢視的物件模型中。 您還沒有匯入資料，所以資料夾是空的。 您可以滑鼠右鍵按一下來執行動作，類似於功能表列物件資料夾。 當您逐步執行本教學課程中，您將使用表格式模型總管 來瀏覽模型專案中的不同的物件。

![as-tabular-lesson1-tme](../analysis-services/media/as-tabular-lesson1-tme.png)

按一下 **方案總管 中** 索引標籤。在這裡，您會看到您**Model.bim**檔案。 如果您看不到左 （含有 [Model.bim] 索引標籤的空視窗），設計工具視窗中**方案總管**下方**AW 網際網路銷售專案**，連按兩下**Model.bim**檔案。 Model.bim 檔案包含所有模型專案的中繼資料。 

![as-tabular-lesson1-se](../analysis-services/media/as-tabular-lesson1-se.png)
  
讓我們看看模型屬性。 按一下 **方案總管**中建立新的空白表格式模型專案。 在 [**屬性**] 視窗中，您會看到[模型屬性](../analysis-services/tabular-models/model-properties-ssas-tabular.md)，最重要的是**DirectQuery 模式**屬性。 此屬性指定模型是以 In-Memory 模式 (關閉) 或是 DirectQuery 模式 (開啟) 部署。 在本教學課程中，您將撰寫及部署記憶體中模式的模型。

![as-tabular-lesson1-properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
當您建立新的模型時，根據資料模型化，可以指定自動設定某些模型屬性**工具** > **選項** 對話方塊。 [資料備份]、[工作空間保留] 和 [工作空間伺服器] 屬性會指定備份、在記憶體中保留以及建立工作空間資料庫 (您的模型撰寫資料庫) 的方式和位置。 您稍後可以視需要變更這些設定，但目前讓這些屬性保持不變。  

在 [**方案總管] 中**，以滑鼠右鍵按一下**AW 網際網路銷售**（專案），然後按一下**屬性**。 **AW 網際網路銷售屬性頁** 對話方塊隨即出現。 這些都是進階[專案屬性](../analysis-services/tabular-models/project-properties-ssas-tabular.md)。 稍後您將在準備好部署模型時，設定其中部分屬性。  
  
當您安裝 SSDT 時，數個新的功能表項目已新增至 Visual Studio 環境中。 讓我們看看與製作表格式模型。 按一下 [模型] 功能表。 從這裡開始，您可以啟動 資料表匯入精靈、 檢視和編輯現有的連接、 重新整理工作區的資料、 瀏覽您在 Excel 中使用 分析 功能的模型、 建立檢視方塊和角色、 選取模型檢視，和設定計算選項。  
  
按一下 [資料表] 功能表。 您可以在此建立及管理資料表之間的關聯性、建立和管理、指定日期資料表設定、建立分割區，以及編輯資料表屬性。  
  
按一下 [資料行] 功能表。 您可以在此於資料表中加入和刪除資料行、凍結資料行，以及指定排序次序。 您也可以使用 [自動加總] 功能為選取的資料行建立標準彙總量值。 其他工具列按鈕可讓您快速存取常用的功能和命令。  
  
瀏覽撰寫表格式模型之各種不同專屬功能的對話方塊和位置。 雖然某些項目還無法使用，但是您仍然可以深入認識表格式模型撰寫環境。  


## <a name="additional-resources"></a>其他資源
若要深入了解不同類型的表格式模型專案，請參閱[表格式模型專案](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)。 若要深入了解表格式模型撰寫環境，請參閱[表格式模型設計師](../analysis-services/tabular-models/tabular-model-designer-ssas.md)。  
  

## <a name="whats-next"></a>下一步
請移至下一課：[第 2 課：將資料加入](../analysis-services/lesson-2-add-data.md)。

  
  
  
