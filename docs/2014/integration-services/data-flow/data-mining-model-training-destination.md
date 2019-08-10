---
title: 資料採礦模型定型目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingmodeltrainingdest.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5dac84fe42185806ae468593876a6bd439c1c689
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890648"
---
# <a name="data-mining-model-training-destination"></a>資料採礦模型定型目的地
  「資料採礦模型培訓」目的地藉由傳送目的地接收的資料至資料採礦模型演算法，來培訓資料採礦模型。 如果多個資料採礦模型建立於同一資料採礦結構上，則可以由一個目的地來培訓這些模型。 如需詳細資訊，請參閱 [採礦結構資料行](https://docs.microsoft.com/analysis-services/data-mining/mining-structure-columns) 和 [採礦模型資料行](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)。  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>設定資料採礦模型培訓目的地  
 如果目標結構和建立於此結構上之模型的案例層級資料行具有 KEY TIME 或 KEY SEQUENCE 類型之內容，則輸入資料必須在該資料行上排序。 例如，使用「Microsoft 時間序列」演算法建立之模型使用的內容類型為 KEY TIME。 如果輸入資料未排序，則模型的處理可能會失敗。 如果資料需要排序，您可使用先前在資料流程中描述的「排序」轉換來排序資料。 此需求不會套用至內容類型為 KEY 的資料行。 如需詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining) 和[排序轉換](transformations/sort-transformation.md)。  
  
> [!NOTE]  
>  「資料採礦模型培訓」目的地的輸入必須排序。 若要排序資料，您可以將「資料採礦模型培訓」目的地上游的「排序」目的地併入資料流程中。 如需詳細資訊，請參閱 [排序轉換](transformations/sort-transformation.md)。  
  
 此目的地有一個輸入，但沒有輸出。  
  
 「資料採礦模型培訓」目的地會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員以連接到包含目的地所培訓之採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [資料採礦模型培訓編輯器] 對話方塊中設定之屬性的詳細資訊，請按一下下列其中一個主題：  
  
-   [資料採礦模型培訓編輯器 &#40;連接索引標籤&#41;](../data-mining-model-training-editor-connection-tab.md)  
  
-   [資料採礦模型培訓編輯器 &#40;資料行索引標籤&#41;](../data-mining-model-training-editor-columns-tab.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [資料採礦模型定型目的地自訂屬性](data-mining-model-training-destination-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)。  
  
  
