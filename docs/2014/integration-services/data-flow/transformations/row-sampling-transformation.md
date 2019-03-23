---
title: 資料列取樣轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowsamplingtrans.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 954e8b2a2f36ccab1cff97174089560913291074
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391236"
---
# <a name="row-sampling-transformation"></a>資料列取樣轉換
  「資料列取樣」轉換是用來取得隨機選取的輸入資料集子集。 您可以指定輸出範例的確實大小，以及指定隨機號碼產生器的種子資料 (Seed)。  
  
 可用於隨機取樣的應用程式有許多種。 例如，某公司希望隨機選取 50 名員工接受抽獎獎項，即可在員工資料庫上使用「資料列取樣」轉換產生正確的獲獎者數目。  
  
 在封裝部署期間，「資料列取樣」轉換對於建立小型但具代表性的資料集來說亦相當實用。 您可以運用豐富的代表性資料測試封裝執行和資料庫轉換，而由於使用隨機取樣而非整個資料集，因此速度更快。 由於測試封裝所使用的取樣資料集大小始終相同，因此使用取樣子集亦可讓識別封裝中的效能問題更為容易。  
  
 此轉換與「百分比取樣」轉換相似，但後者是藉由選取某個百分比的輸入資料列建立取樣資料集。 請參閱 [百分比取樣轉換](percentage-sampling-transformation.md)。  
  
## <a name="configuring-the-row-sampling-transformation"></a>設定資料列取樣轉換  
 「資料列取樣」轉換會藉由選取指定數目的轉換輸入資料列來建立取樣資料集。 由於是從轉換輸入隨機選取資料列，因此結果取樣即為輸入的代表。 您也可以指定隨機號碼產生器使用的種子資料，以影響轉換選取資料列的方式。  
  
 使用相同轉換輸入上的相同隨機種子資料，會固定建立相同的取樣輸出。 如果未指定種子，轉換會使用作業系統的滴答計數建立隨機號碼。 因此，您可以在測試過程中使用相同的種子，以便在開發和測試封裝期間驗證轉換結果，然後在封裝移至實際執行階段時變更為隨機種子。  
  
 資料列取樣轉換包括 `SamplingValue` 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](transformation-custom-properties.md)。  
  
 此轉換有一個輸入和兩個輸出。 但沒有錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [資料列取樣轉換編輯器] 對話方塊中設定之屬性的詳細資訊，請參閱[資料列取樣轉換編輯器 &#40;取樣頁面&#41;](../../row-sampling-transformation-editor-sampling-page.md)。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](../../common-properties.md)  
  
-   [轉換自訂屬性](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>相關工作  
 [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
  
