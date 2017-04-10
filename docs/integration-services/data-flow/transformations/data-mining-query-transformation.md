---
title: "資料採礦查詢轉換 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataminingquerytrans.f1"
helpviewer_keywords: 
  - "資料採礦查詢轉換"
  - "預測查詢 [Integration Services]"
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# 資料採礦查詢轉換
  「資料採礦查詢」轉換會對資料採礦模型執行預測查詢。 這項轉換包含用來建立「資料採礦延伸模組」(DMX) 查詢的查詢產生器。 查詢產生器可讓您建立自訂陳述式，以便使用 DMX 語言對照現有採礦模型評估轉換輸入資料。 如需詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](../../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 如果模型是在相同的資料採礦結構上建立，則一項轉換可執行多項預測查詢。 如需詳細資訊，請參閱[資料採礦查詢工具](../../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
## 設定資料採礦查詢轉換  
 「資料採礦查詢」轉換會使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 連接管理員連接到包含採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 **[資料採礦查詢轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [資料採礦查詢轉換編輯器 &#40;採礦模型索引標籤&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [資料採礦查詢轉換編輯器 &#40;採礦模型索引標籤&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../Topic/Common%20Properties.md)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱[設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
  