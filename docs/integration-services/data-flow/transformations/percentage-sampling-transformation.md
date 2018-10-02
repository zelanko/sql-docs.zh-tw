---
title: 百分比取樣轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.percentagesamplingtrans.f1
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 14292f4d5f1581d02881d565276422b09166de93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631476"
---
# <a name="percentage-sampling-transformation"></a>百分比取樣轉換
  「百分比取樣」轉換會藉由選取轉換輸入資料列的一部分來建立取樣資料集。 取樣資料集是從轉換輸出隨機選取的資料列，用來製作輸入的結果取樣代表。  
  
> [!NOTE]  
>  除了指定的百分比之外，「百分比取樣」轉換還會使用演算法判斷某個資料列是否應包含在取樣輸出中。 這表示取樣輸出中資料列的數目可能不會確實反映指定的百分比。 例如，指定擁有 25,000 個資料列的輸入資料集的 10%，可能不會產生擁有 2,500 個資料列的取樣；取樣的資料列可能會稍微多一點或少一點。  
  
 「百分比取樣」轉換對於資料採礦來說特別實用。 藉由使用此轉換，即可隨機將資料集細分成兩個資料集：一個用於培訓資料採礦模型，另一個用於測試模型。  
  
 「百分比取樣」轉換對於建立封裝開發作業的取樣資料集來說亦相當實用。 藉由套用「百分比取樣」轉換至資料流程，即可一致減少資料集的大小，而同時保留其資料特性。 之後，測試封裝即可更快速地執行，因為它使用更小但更具代表性的資料集。  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>設定轉換取樣率  
 您可以指定取樣種子 (Seed)，以修改轉換用來選取資料列的隨機號碼產生器的行為。 如果使用相同的取樣種子 (Seed)，轉換便會固定產生相同的取樣輸出。 如果未指定種子，轉換會使用作業系統的滴答計數建立隨機號碼。 因此，當您要在開發和測試封裝的過程中驗證轉換結果時，可能會選擇使用標準種子，然後在封裝移至生產時改用隨機種子。  
  
 此轉換與「資料列取樣」轉換相似，但後者是藉由選取指定的輸入資料列數目建立取樣資料集。 如需詳細資訊，請參閱 [資料列取樣轉換](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)。  
  
 百分比取樣轉換包括 **SamplingValue** 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 轉換有一個輸入和兩個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="percentage-sampling-transformation-editor"></a>百分比取樣轉換編輯器
  使用 **[百分比取樣轉換編輯器]** 對話方塊，即可依指定的資料列百分比，將輸入的一部分分割為取樣。 這個轉換會將輸入分成兩個不同的輸出。  
  
### <a name="options"></a>選項。  
 **資料列的百分比**  
 指定在輸入中，要作為取樣的資料列百分比。  
  
 此屬性的值可以使用屬性運算式指定。  
  
 **取樣輸出名稱**  
 提供包含取樣資料列之輸出的唯一名稱。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師內。  
  
 **未選取的輸出名稱**  
 提供輸出的唯一名稱，其中包含從取樣排除的資料列。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師內。  
  
 **使用下列隨機種子**  
 指定轉換用來建立取樣之隨機號碼產生器的取樣種子。 只建議用於開發和測試。 如果未指定隨機種子，轉換會使用 Microsoft Windows 滴答計數。  
  
  
