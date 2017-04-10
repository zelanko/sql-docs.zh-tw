---
title: "檢視 Analysis Services 專案的 XML (SSDT) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
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
  - "專案 [Analysis Services], 檢視 XML"
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# 檢視 Analysis Services 專案的 XML (SSDT)
  當您在專案模式中使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫時，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 會針對專案資料夾中的每一個物件建立 XML 定義。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中檢視每一個物件之 XML 檔案的內容， 您也可以直接編輯 XML 檔案；但是，大多數情況下不建議您這樣做，因為您所做的變更可能會讓 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 無法讀取該 XML 檔案。  
  
> [!NOTE]  
>  您無法檢視整個專案的 xml 程式碼，但是可以檢視每一個物件的程式碼，因為每一個物件都有個別檔案存在。 檢視整個專案之程式碼的唯一方法，就是建立此專案，然後檢視 \<專案名稱>.asdatabase 檔案中的 ASSL 程式碼。  
  
### 檢視物件的 XML 程式碼  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中開啟 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 專案。  
  
2.  以滑鼠右鍵按一下方案總管中的物件，然後按一下 [檢視程式碼]。  
  
     此物件的 XML 程式碼即會出現在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中。  
  
## 請參閱＜  
 [建立多個 Analysis Services 專案 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  