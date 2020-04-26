---
title: 修改預測結構（元資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63301296"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>修改預測結構 (中繼資料採礦教學課程)
  上一項工作所建立的採礦結構包含單一預測模型。 在處理和瀏覽這個模型之前，您必須先稍微變更它的結構，並修改其中一個屬性。  
  
## <a name="modifying-the-mining-structure"></a>修改採礦結構  
 您可以使用資料採礦設計師的 [**採礦結構**] 索引標籤來變更此採礦結構。 當您使用資料採礦精靈建立此模型時，會使用三個資料行：ReportingDate、ModelRegion 和 Quantity。 不過，[**預測**] 資料表也包含 [金額] 資料行，您可以用來預測銷售金額。 藉由使用 [**採礦結構**] 索引標籤，您可以將此資料行從 [資料來源] 視圖加入至 [採礦結構]。  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>若要將 [金額] 資料行加入預測採礦結構中  
  
1.  在資料採礦設計師的 [**採礦結構**] 索引標籤上，于 [**資料來源視圖**] 窗格中，選取 [vTimeSeries] 資料表中的 [金額] 資料行。  
  
2.  從 [**資料來源視圖**] 窗格中，將 [金額] 資料行拖曳至**預測**結構的資料行清單中。  
  
     [金額] 資料行現在已包含在**預測**採礦結構中。  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>修改採礦模型中的資料行  
 由於您在結構中加入了新的資料行，因此，您必須定義模型使用這個資料行的方式。 您可以在資料採礦設計師的 [**採礦模型**] 索引標籤上，指定資料行的使用方式。  
  
 [**採礦模型**] 索引標籤會在方格的 [**結構**] 資料行中列出採礦結構所包含的資料行，並在具有模型名稱的資料行中列出該採礦模型所包含的資料行（在此案例中為**預測**）。 請按一下資料行的名稱來加以修改。 在 [**預測**] 採礦模型中，[金額] 資料行會當做輸入資料行使用，也可用來預測未來的銷售。 因此，您必須設定資料行的屬性，使它既能做為輸入資料行，也能做為可預測資料行。  
  
> [!NOTE]  
>  在 [**採礦模型**] 索引標籤中，您也可以建立以相同結構為基礎的新模型，而且您可以調整每個模型的演算法和資料行屬性。 不過，您必須先處理模型，然後這些變更才會生效。  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>若要定義 [金額] 資料行的使用方式  
  
1.  在 [**採礦模型**] 索引標籤上方格的 [**預測**] 資料行中，按一下 [金額] 資料列中的資料格。  
  
2.  從清單中選取 [**預測**]。  
  
     現在，Amount 資料行既是輸入資料行，也是可預測資料行。  
  
 您也可以選取資料行並開啟 [**屬性**] 視窗，以變更個別資料行的屬性。 若要開啟 [**屬性**] 視窗，請以滑鼠右鍵按一下資料行名稱，然後選取 [**屬性**]。 如果您變更個別模型的資料行屬性，您只能變更這個模型的屬性。 不過，當您變更 [**結構**] 資料行中的屬性時，變更會影響與該結構相關聯的每個模型。 每當變更模型或結構之後，都必須重新處理才能讓變更生效。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [自訂及處理預測模型 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Analysis Services 的採礦結構-資料採礦&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [採礦模型 &#40;Analysis Services - 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
