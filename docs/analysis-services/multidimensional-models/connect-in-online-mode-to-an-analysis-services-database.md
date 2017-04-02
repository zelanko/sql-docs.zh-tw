---
title: "在連線模式下連接至 Analysis Services 資料庫 | Microsoft Docs"
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
  - "Analysis Services, 連接"
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# 在連線模式下連接至 Analysis Services 資料庫
  您可以直接連接到現有的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫，並直接修改該資料庫中的物件。 當您直接連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，對物件的變更會立即發生，而且 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中不會建立任何 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]專案。  
  
### 若要使用 SQL Server 資料工具直接連接到 Analysis Services 資料庫  
  
1.  開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
2.  指向 **[檔案]** 功能表上的 **[開啟舊檔]** ，再按一下 **[Analysis Services 資料庫]**。  
  
3.  選取 **[連接到現有的資料庫]**。  
  
4.  指定伺服器名稱和資料庫名稱。  
  
     您可以輸入資料庫名稱或是查詢伺服器，以檢視伺服器上現有的資料庫。  
  
5.  按一下 **[確定]**。  
  
     您現在可以直接編輯 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的任何物件。  
  
## 請參閱＜  
 [在開發階段使用 Analysis Services 專案和資料庫](../../analysis-services/multidimensional-models/work-with-analysis-services-projects-and-databases-in-development.md)   
 [使用 SQL Server 資料工具建立多維度模型 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  