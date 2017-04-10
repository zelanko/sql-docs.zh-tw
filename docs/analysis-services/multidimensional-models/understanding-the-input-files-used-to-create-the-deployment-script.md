---
title: "了解用來建立部署指令碼的輸入檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "輸入檔 [Analysis Services]"
  - "Analysis Services 部署精靈，指令碼"
  - "部署 [Analysis Services], 輸入檔"
  - "Analysis Services 部署精靈, 輸入檔"
  - "指令碼 [Analysis Services], 部署"
  - "Analysis Services 部署, 輸入檔"
  - "修改輸入檔"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 了解用來建立部署指令碼的輸入檔
  當您建置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會為專案產生 XML 檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會將這些 XML 檔案放置在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的輸出資料夾中。 依預設，輸出是放在 \\Bin 資料夾中。 下表列出 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 建立的 XML 檔案。  
  
|XMLA 檔案|說明|  
|---------------|-----------------|  
|\<*專案名稱*\>.asdatabase|包含專案中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的宣告式定義。|  
|\<*專案名稱*\>.deploymenttargets|包含將建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫的名稱。|  
|\<*專案名稱*\>.configsettings|包含環境特定設定，例如資料來源連接資訊和物件儲存位置。 此檔案中的設定會覆寫 \<*專案名稱*\>.asdatabase 檔案中的設定。|  
|\<*專案名稱*\>.deploymentoptions|包含部署選項，例如部署是否為交易式，以及部署之後是否應處理部署的物件。|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 絕不會將密碼儲存在專案檔中。  
  
## 修改輸入檔  
 修改輸入檔中的值，或從輸入檔中擷取值，就可以變更部署目的地、組態設定和部署選項，而不用編輯整個 \<*專案名稱*\>.asdatabase 檔案 \(如果是從現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫產生指令碼，則為整個 XMLA 指令碼檔案\)。 您可以修改個別的檔案，以輕鬆地針對各種用途建立不同的部署指令碼。  
  
 下列主題說明如何修改各種輸入檔中的值：  
  
-   [指定安裝目標](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [指定資料分割和角色部署選項](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [指定方案部署的組態設定](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [指定處理選項](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## 另請參閱  
 [執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解 Analysis Services 部署指令碼](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  