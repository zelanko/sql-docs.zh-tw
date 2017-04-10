---
title: "將屬性加入維度中 | Microsoft Docs"
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
  - "加入屬性"
  - "自動建立屬性"
  - "屬性 [Analysis Services], 建立"
  - "屬性 [Analysis Services], 加入"
  - "手動建立屬性 [Analysis Services]"
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 將屬性加入維度中
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以手動或自動將屬性加入至維度中。  
  
 若要自動建立屬性，在 **之維度設計師的** [維度結構] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]索引標籤上，選取您要對應到屬性的資料行，然後從 **[資料來源檢視]** 窗格中將該資料行拖曳至 **[屬性]** 窗格中。 這樣會建立一個對應到該資料行的屬性，並將資料行的相同名稱指定給屬性。 如果已有使用該名稱的屬性， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會對第一個重複名稱加入從 "1" 開始的序號後置詞。  
  
 若要手動建立屬性，請將 **[屬性]** 窗格設為方格檢視。 在方格最後一個資料列的名稱資料行中，按一下 [\<新屬性>] 項目。 輸入新屬性的名稱。 這樣子所建立的屬性，不對應到其所有屬性均為預設值的資料行。 您可以在 **的** [屬性] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 視窗中，設定新屬性的 **KeyColumns** 屬性來設定對應。  
  
 如需詳細資訊，請參閱[自動定義新屬性](../../analysis-services/multidimensional-models/define-a-new-attribute-automatically.md)、[手動定義新屬性](../Topic/Define%20a%20New%20Attribute%20Manually.md)、[繫結屬性與名稱資料行](../../analysis-services/multidimensional-models/bind-an-attribute-to-a-name-column.md)及[修改屬性 (attribute) 的 KeyColumn 屬性 (property)](../../analysis-services/multidimensional-models/modify-the-keycolumn-property-of-an-attribute.md)。  
  
## 請參閱＜  
 [維度屬性 (Attribute) 屬性 (Property) 參考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  