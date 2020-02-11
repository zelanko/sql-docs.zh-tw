---
title: 指定定型資料（資料採礦嚮導） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3bbeb708cdb0c2882b85d55081446b3dc12b56b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068070"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>指定培訓資料 (資料採礦精靈)
  使用 [指定定型資料]**** 頁面，即可識別要在採礦結構中包含什麼資料行。 您可以選取要包含在結構中的資料行，即使不會在所有模型中使用也是如此。 例如，如果想要從採礦模型鑽研資料行，則可將這些資料行包含在結構中 (而非模型中)。  
  
 包含在結構中的每個資料表都至少需要一個索引鍵資料行。 您挑選為索引鍵的資料行是根據資料表是案例資料表或巢狀資料表而定。 如果資料表是巢狀資料表，則索引鍵通常是可預測的資料行，而不是關聯的外部索引鍵。 若要深入了解巢狀索引鍵，請參閱[巢狀資料表 &#40;Analysis Services - 資料採礦&#41;](data-mining/nested-tables-analysis-services-data-mining.md)。  
  
> [!NOTE]  
>  不同的採礦演算法會以不同的方式使用索引鍵。 若要深入了解不同種類的索引鍵，請參閱[內容類型 &#40;資料採礦&#41;](data-mining/content-types-data-mining.md)。  
  
 **如需詳細資訊：** [&#40;Analysis Services 的採礦結構、資料採礦&#41;](data-mining/mining-structures-analysis-services-data-mining.md)、「[採礦模型資料行](data-mining/mining-model-columns.md)」、「[資料採礦嚮導」 &#40;Analysis Services 資料採礦&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)、[建立關聯式的採礦結構](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>選項。  
 **資料表/資料行**  
 顯示在精靈的上一頁上所選取的資料表和資料行。  
  
 **\<核取方塊>**  
 選取要包含在採礦結構中的資料行。  
  
 如果資料來源包含巢狀資料表或多個檢視，請展開資料行清單來檢視巢狀資料表。  
  
 **索引鍵**  
 選取即可使用資料行作為資料的唯一識別碼。  
  
 對案例資料表而言，索引鍵通常是唯一識別碼。  
  
 對巢狀資料表而言，[索引鍵]**** 指出相關聯案例內容中之資料列的識別碼。  
  
 **輸入**  
 選取即可在建立預測時使用資料行。  
  
> [!NOTE]  
>  只有在建立採礦模型時同時建立採礦結構，才可以使用這個資料行。  
  
 **可預測**  
 選取即可啟用依據其他未來的輸入，來預測資料表或資料行。  
  
 如果您也將巢狀資料表標示為可預測，則整個巢狀資料表會變成可預測。 如果巢狀資料表中沒有資料行標示為輸入或可預測，巢狀資料表就會出現在採礦結構中，但是在模型中會被忽略。  
  
 **注意**此資料行只有在您同時建立了與此採礦結構的採礦模型時才可使用。  
  
 **建議**  
 按一下即可開啟 [建議相關資料行]**** 對話方塊，它會對採樣資料進行分析，來識別與依據 Entropy 所選取 [可預測]**** 資料行展現最大關聯性的輸入資料行。 此分析也適用於以 OLAP 來源為基礎的巢狀資料表資料行或採礦結構。  
  
 **注意**此資料行僅適用于當您建立與該採礦結構的整合模型時。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦嚮導 F1 說明 &#40;Analysis Services-資料採礦&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [建議相關資料行 &#40;Data 採集 Wizard&#41;](suggest-related-columns-data-mining-wizard.md)   
 [指定資料表類型 &#40;資料採礦嚮導&#41;](specify-table-types-data-mining-wizard.md)   
 [指定資料行的內容和資料類型 &#40;[Data] [Wizard]&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
