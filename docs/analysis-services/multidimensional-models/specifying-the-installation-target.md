---
title: "指定安裝目標 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "輸入檔 [Analysis Services]"
  - "安裝目標 [Analysis Services]"
  - "Analysis Services 部署, 安裝目標"
  - "Analysis Services 部署精靈, 安裝目標"
  - "部署 [Analysis Services], 安裝目標"
  - "修改安裝目標"
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 指定安裝目標
  [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 會從 \<專案名稱>.deploymenttargets 檔案中讀取安裝目標資訊。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 當您建立 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，下列項目會建立此檔案： [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會使用 \<專案名稱>[屬性頁面] 對話方塊之 [部署] 頁面上指定的資料庫和伺服器來建立 \<專案名稱>.targets 檔案。  
  
## 修改部署的安裝目標  
 在某些情況下，您可能需要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到與 [部署] 頁面所指定之不同的資料庫或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上。 例如，您可能需要在部署之前先將專案部署到伺服器以進行測試，然後在測試完成後再部署到實際伺服器。 您也可能需要將完整與測試的專案部署到網路負載平衡叢集中的多個實際伺服器，或部署到臨時伺服器和實際伺服器。  
  
 若要將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案部署到不同的資料庫或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體，您可以使用下列程序描述的方法之一，來變更輸入檔中的安裝目標。  
  
#### 若要在已產生輸入檔之後，變更安裝目標  
  
-   以互動方式執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。 在 [安裝目標] 頁面上，指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫的新目的地。  
  
     – 或 –  
  
-   在命令提示字元下執行 [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈]，並將精靈設定為以回應檔案模式執行。 如需回應檔案模式的詳細資訊，請參閱[執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。  
  
     – 或 –  
  
-   使用任何文字編輯器來修改 \<專案名稱>.deploymenttargets 檔案。  
  
## 請參閱＜  
 [指定資料分割和角色部署選項](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [指定方案部署的組態設定](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [指定處理選項](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  