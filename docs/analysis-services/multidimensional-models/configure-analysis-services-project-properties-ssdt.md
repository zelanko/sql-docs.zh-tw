---
title: "設定 Analysis Services 專案屬性 (SSDT) | Microsoft Docs"
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
f1_keywords: 
  - "VS.TOOLSOPTIONSPAGES.BUSINESS_INTELLIGENCE_DESIGNERS.ANALYSIS_SERVICES_DESIGNERS.GENERAL"
helpviewer_keywords: 
  - "專案 [Analysis Services], 屬性"
ms.assetid: d9786c66-7d8c-48e3-950d-3f25044b4ce2
caps.latest.revision: 24
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 24
---
# 設定 Analysis Services 專案屬性 (SSDT)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，將會包含一些影響 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案建立及部署的預設屬性。  
  
 若要變更專案屬性，請以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案物件，然後按一下 [屬性]。 或者，您可以在 [專案] 功能表上，按一下 [屬性]。  
  
## 屬性描述  
 下表描述的是每一個專案屬性、列出其預設值，以及提供變更屬性值的詳細資訊。  
  
|屬性|預設值|說明|  
|--------------|---------------------|-----------------|  
|建立 / 部署伺服器版本|用來開發專案的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|指定最終會將專案部署到哪一個版本的伺服器。 當與專案的多位開發人員合作時，開發人員需要了解伺服器版本，才能知道哪些功能會併入到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案中。|  
|建立 / 部署伺服器版本|用來開發專案的版本|指定最終會將專案部署到哪一個版本的伺服器。|  
|建立 / 輸出|/bin|專案建立程序之輸出的相對路徑|  
|建立 / 移除密碼|True|指定在建立程序期間寫入輸出目錄的連接字串中，是否要移除已知的密碼。 移除密碼是為了增加安全性； 如果移除密碼，當處理已部署的專案時，將需要提供密碼，好讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 能夠存取來源資料。|  
|偵錯 / 起始物件|\<目前使用中的物件>|決定當您開始偵錯時所要起始的物件。|  
|部署 / 部署模式|只部署變更|依預設，只會部署對專案物件所做的變更 (前提是未直接在專案外面對物件進行其他變更)。 您也可以選擇在每一次部署期間部署所有專案物件。 為了獲得最佳效能，請使用 [只部署變更]。|  
|部署 / 處理選項|預設值|依預設，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在部署物件變更時決定所需的處理類型， 這通常會產生最快的部署時間； 但是，您也可以選擇在每一次部署時進行完整的處理或是不執行任何處理。|  
|部署 / 交易式部署|False|依預設，在處理已部署的物件時，已變更之物件或所有物件的部署並不是交易式部署。 即使處理失敗，部署仍可以成功，並持續存在。 您可以變更這項預設值，在單一交易中併入部署和處理。|  
|部署 / 目標伺服器|localhost|依預設，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案內的資料庫物件將會部署到使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 之本機電腦上的預設 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 變更這項預設值，以便在本機電腦上或是您有權建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件之任何遠端電腦上的任何執行個體上指定具名執行個體。|  
|部署 / 資料庫|\<專案名稱>|依預設，一旦部署之後，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案物件會立刻具現化所在的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫名稱就是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案定義時的名稱。 請變更這個屬性，以變更伺服器屬性所指定之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上的資料庫名稱。|  
  
## 屬性組態  
 屬性的定義是以每一個組態為原則； 專案組態可讓開發人員在不同的建立、偵錯和部署設定之下處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案，而不需要直接編輯基礎 XML 專案檔案。  
  
 專案一開始是以單一組態 (稱為「開發」) 來建立； 您可以使用組態管理員建立其他組態，並在不同的組態之間切換。  
  
 在建立其他組態之前，所有開發人員都會使用這個共同的組態； 但是，在專案開發的各個不同階段期間 (例如，在最初開發專案及測試專案期間)，不同的開發人員可能會使用不同的資料來源，並針對不同用途將此專案部署到不同的伺服器； 組態可讓您保留不同組態檔內的這些不同設定。  
  
## 請參閱＜  
 [建立 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [部署 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  