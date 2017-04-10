---
title: "第 14 課：部署 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 14 課：部署
在這一課，您將設定部署屬性：指定以 [表格式] 模式執行之 Analysis Services 的部署伺服器執行個體，以及您所部署模型的名稱。 接著將模型部署至該執行個體。 部署完成後，使用者就可以使用報表用戶端應用程式連接到此模型。 如需詳細資訊，請參閱[表格式模型方案部署 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
完成本課程的估計時間：**5 分鐘**  
  
## 必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課程的工作之前，您應已完成上一課：[第 13 課：在 Excel 中進行分析](../analysis-services/lesson-13-analyze-in-excel.md)。  
  
## 部署模型  
  
#### 若要設定部署屬性  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的**方案總管**中，以滑鼠右鍵按一下 **Adventure Works Internet Sales Tabular Model** 專案，然後在操作功能表中按一下 [屬性]。  
  
2.  在 [AW Internet Sales Tabular Model 屬性頁] 對話方塊中的 [部署伺服器] 底下，於 [伺服器] 屬性中輸入以表格式模式執行的 Analysis Services 執行個體名稱。 您會將模型部署到這個執行個體中。  
  
    > [!IMPORTANT]  
    > 您必須具有遠端 Analysis Services 執行個體的系統管理員權限，才能部署到該執行個體。  
  
3.  在 **Database** 屬性中，輸入 **Adventure Works Internet Sales Model**。  
  
4.  在 **Cube** 名稱屬性中，輸入 **Adventure Works Internet Sales Model**。  
  
5.  確認您的選取，然後按一下 [確定]。  
  
#### 若要部署 Adventure Works Internet Sales 表格式模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，按一下 [建立] 功能表，然後按一下 [Deploy AW Internet Sales Tabular Model (部署 AW Internet Sales Tabular Model)]。  
  
    [部署] 對話方塊隨即出現，並且顯示中繼資料以及模型中每個資料表的部署狀態。  
  
2. 當部署順利完成時，就可以按一下 [關閉]。  
  
## 結論  
恭喜！ 您已完成撰寫和部署第一個 Analysis Services 表格式模型。 本教學課程已幫助您完成建立表格式模型最常執行的工作。 現在您已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 管理此模型，並且建立處理序指令碼及備份計畫。 使用者可以使用報表用戶端應用程式 (例如 Microsoft Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]) 連接到此模型。  
  
## 其他資源  
若要深入了解支援 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 報表的表格式模型屬性，請參閱 [Power View 報表屬性 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)。  
  
## 另請參閱  
[DirectQuery 模式 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[設定預設的資料模型和部署屬性 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[表格式模型資料庫 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  
