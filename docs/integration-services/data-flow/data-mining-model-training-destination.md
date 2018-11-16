---
title: 資料採礦模型定型目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fda41af4bbf9f6e0b98de5c543af99e732966d53
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51640485"
---
# <a name="data-mining-model-training-destination"></a>資料採礦模型定型目的地
  「資料採礦模型培訓」目的地藉由傳送目的地接收的資料至資料採礦模型演算法，來培訓資料採礦模型。 如果多個資料採礦模型建立於同一資料採礦結構上，則可以由一個目的地來培訓這些模型。 如需詳細資訊，請參閱 [採礦結構資料行](../../analysis-services/data-mining/mining-structure-columns.md) 和 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)。  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>設定資料採礦模型培訓目的地  
 如果目標結構和建立於此結構上之模型的案例層級資料行具有 KEY TIME 或 KEY SEQUENCE 類型之內容，則輸入資料必須在該資料行上排序。 例如，使用「Microsoft 時間序列」演算法建立之模型使用的內容類型為 KEY TIME。 如果輸入資料未排序，則模型的處理可能會失敗。 如果資料需要排序，您可使用先前在資料流程中描述的「排序」轉換來排序資料。 此需求不會套用至內容類型為 KEY 的資料行。 如需詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md) 和[排序轉換](../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
> [!NOTE]  
>  「資料採礦模型培訓」目的地的輸入必須排序。 若要排序資料，您可以將「資料採礦模型培訓」目的地上游的「排序」目的地併入資料流程中。 如需詳細資訊，請參閱 [排序轉換](../../integration-services/data-flow/transformations/sort-transformation.md)。  
  
 此目的地有一個輸入，但沒有輸出。  
  
 「資料採礦模型培訓」目的地會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連線管理員以連接到包含目的地所培訓之採礦結構和採礦模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體。 如需相關資訊，請參閱 [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [資料採礦模型定型目的地自訂屬性](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>資料採礦模型培訓編輯器 (連接索引標籤)
  使用 **[資料採礦模型培訓編輯器]** 對話方塊的 **[連接]** 頁面，選取要培訓的採礦模型。  
  
### <a name="options"></a>選項。  
 **[ODBC 目的地編輯器]**  
 從現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接清單中進行選取，或使用 [新增] 按鈕建立新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接，如下所述。  
  
 **新增**  
 使用 [加入 Analysis Services 連接管理員] 對話方塊來建立新的連接。  
  
 **採礦結構**  
 從可用的採礦結構清單中選取，或按一下 [新增] 建立新結構。  
  
 **新增**  
 使用 [資料採礦精靈] 來建立新的採礦結構和採礦模型。  
  
 **採礦模型**  
 檢視與選取的採礦結構相關聯的採礦模型清單。  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>資料採礦模型培訓編輯器 (資料行索引標籤)
  使用 **[資料採礦模型培訓編輯器]** 對話方塊的 **[資料行]** 頁面，即可將輸入資料行對應至採礦結構的資料行。  
  
## <a name="options"></a>選項。  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。 拖曳輸入資料行以對應至採礦結構資料行。  
  
 **採礦結構資料行**  
 檢視採礦結構資料行的清單。 拖曳採礦結構資料行以對應至可用的輸入資料行。  
  
 **輸入資料行**  
 從上述資料表檢視選取的輸入資料行。 若要變更或移除對應選擇，請使用 **[可用的輸入資料行]** 清單。  
  
 **採礦結構資料行**  
 檢視每個可用的目的地資料行，不論是否已經對應。  
  
