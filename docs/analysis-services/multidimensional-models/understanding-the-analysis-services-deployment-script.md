---
title: "了解 Analysis Services 部署指令碼 | Microsoft Docs"
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
  - "Analysis Services 部署精靈，指令碼"
  - "部署 [Analysis Services], 指令碼"
  - "Analysis Services 部署, 指令碼"
  - "指令碼 [Analysis Services], 部署"
ms.assetid: a63ebee9-9848-48f1-82ad-64ecf2e47019
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 31
---
# 了解 Analysis Services 部署指令碼
  [[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈] 產生的 XMLA 部署指令碼包含兩個區段：  
  
-   部署指令碼的第一個部分包含要建立、改變或刪除目的地資料庫中的適當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件時所需的命令。 根據預設，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案產生的輸入檔是以累加部署為基礎。 因此，XMLA 部署指令碼將只會影響已變更或刪除的物件。  
  
-   部署指令碼的第二個部分包含僅要處理目的地伺服器上所建立或改變的物件時所需的命令 ([處理預設] 選項) 或完整處理目的地資料庫時所需的命令。 您也可以選擇讓部署指令碼不包含任何處理命令。  
  
 整個部署指令碼可在單一交易或多筆交易中執行。 如果指令碼在多筆交易中執行，指令碼的第一個部分會以單一交易執行，而每一個物件會在它自己的交易中處理。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈只會將物件部署到單一 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。 它不會部署任何伺服器層級的物件或資料。  
  
## 請參閱＜  
 [執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)  
  
  