---
title: 百分比取樣轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.percentagesamplingtrans.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09e8a4a4ccf4b6e018e8c8ef4a905f77e417b3e9
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437585"
---
# <a name="percentage-sampling-transformation"></a>百分比取樣轉換
  「百分比取樣」轉換會藉由選取轉換輸入資料列的一部分來建立取樣資料集。 取樣資料集是從轉換輸出隨機選取的資料列，用來製作輸入的結果取樣代表。  
  
> [!NOTE]  
>  除了指定的百分比之外，「百分比取樣」轉換還會使用演算法判斷某個資料列是否應包含在取樣輸出中。 這表示取樣輸出中資料列的數目可能不會確實反映指定的百分比。 例如，指定擁有 25,000 個資料列的輸入資料集的 10%，可能不會產生擁有 2,500 個資料列的取樣；取樣的資料列可能會稍微多一點或少一點。  
  
 「百分比取樣」轉換對於資料採礦來說特別實用。 藉由使用此轉換，即可隨機將資料集細分成兩個資料集：一個用於培訓資料採礦模型，另一個用於測試模型。  
  
 「百分比取樣」轉換對於建立封裝開發作業的取樣資料集來說亦相當實用。 藉由套用「百分比取樣」轉換至資料流程，即可一致減少資料集的大小，而同時保留其資料特性。 之後，測試封裝即可更快速地執行，因為它使用更小但更具代表性的資料集。  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>設定轉換取樣率  
 您可以指定取樣種子 (Seed)，以修改轉換用來選取資料列的隨機號碼產生器的行為。 如果使用相同的取樣種子 (Seed)，轉換便會固定產生相同的取樣輸出。 如果未指定種子，轉換會使用作業系統的滴答計數建立隨機號碼。 因此，當您要在開發和測試封裝的過程中驗證轉換結果時，可能會選擇使用標準種子，然後在封裝移至生產時改用隨機種子。  
  
 此轉換與「資料列取樣」轉換相似，但後者是藉由選取指定的輸入資料列數目建立取樣資料集。 如需詳細資訊，請參閱 [資料列取樣轉換](row-sampling-transformation.md)。  
  
 百分比取樣轉換包括 `SamplingValue` 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](transformation-custom-properties.md)。  
  
 轉換有一個輸入和兩個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [百分比取樣轉換編輯器]**** 對話方塊中設定之屬性的詳細資訊，請參閱[百分比取樣轉換編輯器](../../percentage-sampling-transformation-editor.md)。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
 如需如何設定屬性的詳細資訊，請參閱 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)。  
  
  
