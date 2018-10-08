---
title: 資料採礦查詢轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de863a5aeba65dded46990d94e204bb29ef6bd1c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813066"
---
# <a name="data-mining-query-transformation"></a>資料採礦查詢轉換
  「資料採礦查詢」轉換會對資料採礦模型執行預測查詢。 這項轉換包含用來建立「資料採礦延伸模組」(DMX) 查詢的查詢產生器。 查詢產生器可讓您建立自訂陳述式，以便使用 DMX 語言對照現有採礦模型評估轉換輸入資料。 如需詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](../../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 如果模型是在相同的資料採礦結構上建立，則一項轉換可執行多項預測查詢。 如需詳細資訊，請參閱 [資料採礦查詢工具](../../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>設定資料採礦查詢轉換  
 「資料採礦查詢」轉換會使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 連接管理員連接到包含採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>資料採礦查詢轉換編輯器 (採礦模型索引標籤)
  使用 **[資料採礦查詢轉換編輯器]** 對話方塊的 **[採礦模型]** 索引標籤，來選取資料採礦結構及其採礦模型。  
  
### <a name="options"></a>選項。  
 **[連接]**  
 使用清單方塊來選取現有的 Analysis Services 連接，或使用 [新增] 按鈕來建立新的連接，如下所述。  
  
 **新增**  
 使用 [加入 Analysis Services 連接管理員] 對話方塊來建立新的連接。  
  
 **採礦結構**  
 從可用之採礦模型結構的清單中選取。  
  
 **採礦模型**  
 檢視與選取的資料採礦結構相關聯的採礦模型清單。  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>資料採礦查詢轉換編輯器 (查詢索引標籤)
  使用 **[資料採礦查詢轉換編輯器]** 對話方塊的 **[查詢]** 索引標籤，即可建立預測查詢。  
  
### <a name="options"></a>選項。  
 **資料採礦查詢**  
 將資料採礦延伸模組 (DMX) 查詢直接輸入文字方塊中。  
  
 **建立新查詢**  
 按一下 [建立新查詢]，即可使用圖形化查詢產生器建立資料採礦延伸模組 (DMX) 查詢。  
  
