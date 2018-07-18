---
title: 修改預測結構 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e2605e5ab2c36c282adec778f6f20ebb2e37f1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189415"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>修改預測結構 (中繼資料採礦教學課程)
  上一項工作所建立的採礦結構包含單一預測模型。 在處理和瀏覽這個模型之前，您必須先稍微變更它的結構，並修改其中一個屬性。  
  
## <a name="modifying-the-mining-structure"></a>修改採礦結構  
 您可以使用來變更採礦結構**採礦結構**資料採礦設計師 索引標籤。 當您使用資料採礦精靈建立此模型時，會使用三個資料行：ReportingDate、ModelRegion 和 Quantity。 不過，**預測**資料表也包含 Amount 資料行，您可用於預測銷售金額。 藉由使用**採礦結構**索引標籤上，將此資料行從資料來源檢視加入至採礦結構。  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>若要將 [金額] 資料行加入預測採礦結構中  
  
1.  上**Mining Structure**  索引標籤的 資料採礦設計師中**資料來源檢視** 窗格中，選取 vTimeSeries 資料表中的 Amount 資料行。  
  
2.  拖曳 [金額] 資料行從**資料來源檢視**窗格將資料行清單**預測**結構。  
  
     Amount 資料行現在已包含在**預測**採礦結構。  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>修改採礦模型中的資料行  
 由於您在結構中加入了新的資料行，因此，您必須定義模型使用這個資料行的方式。 您可以指定資料行上的使用方式**採礦模型**資料採礦設計師 索引標籤。  
  
 **採礦模型**索引標籤會列出採礦結構中包含的資料行**結構**的方格，並列出採礦模型包含具有名稱的資料行中的資料行的資料行建立模型，在此情況下**預測**。 請按一下資料行的名稱來加以修改。 在 **預測**採礦模型中，Amount 資料行做為輸入資料行，並也會用來預測未來的銷售。 因此，您必須設定資料行的屬性，使它既能做為輸入資料行，也能做為可預測資料行。  
  
> [!NOTE]  
>  在 **採礦模型**索引標籤上，您可以建立新的模型根據相同的結構，且您可以調整每個模型的演算法和資料行屬性。 不過，您必須先處理模型，然後這些變更才會生效。  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>若要定義 [金額] 資料行的使用方式  
  
1.  在  **Forecasting**上方格的資料行**採礦模型**索引標籤上，按一下 Amount 資料列中的資料格。  
  
2.  選取  **Predict**從清單中。  
  
     現在，Amount 資料行既是輸入資料行，也是可預測資料行。  
  
 您也可以變更個別資料行的屬性，選取資料行，並開啟**屬性**視窗。 若要開啟 [**屬性**] 視窗中，以滑鼠右鍵按一下資料行名稱，然後按**屬性**。 如果您變更個別模型的資料行屬性，您只能變更這個模型的屬性。 不過，當您變更內的屬性**結構** 欄中，變更會影響與結構相關聯的每個模型。 每當變更模型或結構之後，都必須重新處理才能讓變更生效。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [自訂及處理預測模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [採礦模型&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
