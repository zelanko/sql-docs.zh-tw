---
title: 資料採礦查詢轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d9ab528b290fdbba841a1a8acf56f1f4f01c8fec
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375486"
---
# <a name="data-mining-query-transformation"></a>資料採礦查詢轉換
  「資料採礦查詢」轉換會對資料採礦模型執行預測查詢。 這項轉換包含用來建立「資料採礦延伸模組」(DMX) 查詢的查詢產生器。 查詢產生器可讓您建立自訂陳述式，以便使用 DMX 語言對照現有採礦模型評估轉換輸入資料。 如需詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)。  
  
 如果模型是在相同的資料採礦結構上建立，則一項轉換可執行多項預測查詢。 如需詳細資訊，請參閱 <<c0> [ 資料採礦查詢介面](../../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>設定資料採礦查詢轉換  
 「資料採礦查詢」轉換會使用 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 連接管理員連接到包含採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../connection-manager/analysis-services-connection-manager.md)。  
  
 此轉換有一個輸入和一個輸出。 它不支援錯誤輸出。  
  
 您可以透過「 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 **[資料採礦查詢轉換編輯器]** 對話方塊中設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [資料採礦查詢轉換編輯器 &#40;採礦模型索引標籤&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [資料採礦查詢轉換編輯器 &#40;採礦模型索引標籤&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
