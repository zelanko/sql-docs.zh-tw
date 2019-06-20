---
title: 巢狀資料表 (Analysis Services-資料採礦) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 35444ae17ac4a11bd0321e70631f45d84273e0af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62472404"
---
# <a name="nested-tables-analysis-services---data-mining"></a>巢狀資料表 (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料必須當作包含在案例資料表內的一系列案例，傳送至資料採礦演算法。 不過，並非所有的案例都可以由單一資料列描述。 例如，案例可能從兩個資料表衍生：一個資料表包含客戶資訊，而另一個資料表包含客戶購買資訊。 客戶資訊表中的單一客戶在客戶購買資料表中可能有多筆購買項目，所以很難以單一資料列描述資料。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供獨特方法來處理這些情況下，就使用*巢狀資料表*。 下圖展示巢狀資料表的概念。  
  
 ![兩個資料表使用巢狀的資料表結合](../../analysis-services/data-mining/media/nested-tables.gif "兩個資料表合併使用巢狀的資料表")  
  
 在此圖表中，第一個資料表 (父資料表) 包含客戶相關資訊，且每一位客戶有唯一識別碼的關聯。 第二個資料表 (子資料表) 包含每一位客戶的購買資訊。 子資料表中的購買資訊會經由唯一識別碼 **CustomerKey** 資料行，與父資料表產生關聯。 圖表中的第三個資料表會顯示這兩個資料表的結合。  
  
 巢狀資料表會以案例資料表中的特殊資料行表示，此資料行的資料類型為 **TABLE**。 針對任何特定的案例資料列，這種資料行包含從子資料表中選取與父資料表有關的資料列。  
  
 巢狀資料表中的資料可以用於預測或輸入，或同時用於兩者。 例如，您可能有兩個巢狀資料表資料行在一個模型中：一個巢狀資料表資料行可能包含客戶已購買的產品清單，而另一個巢狀資料表則包含調查到的客戶嗜好與興趣資訊。 在此案例中，您可以使用客戶的嗜好與興趣，做為分析購買行為以及預測可能購買產品的輸入。  
  
## <a name="joining-case-tables-and-nested-tables"></a>聯結案例資料表和巢狀資料表  
 為了建立巢狀資料表，兩個來源資料表必須包含已定義的關聯性，讓一個資料表中的項目可以與另一個資料表相關。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，您可以在資料來源檢視內定義此關聯性。  
  
> [!NOTE]  
>  **CustomerKey** 欄位是關聯式索引鍵，用於在資料來源檢視定義內連結案例資料表和巢狀資料表，以及在採礦結構內建立資料行的關聯性。 不過，一般而言，您不應該在建立於該結構上的採礦模型中使用此關聯式索引鍵。 如果關聯式索引鍵資料行只用於聯結資料表，而不會提供對於分析有用的資訊，則通常最好將它從採礦模型內去除。  
  
 您可以使用資料採礦延伸模組 (DMX) 或分析管理物件 (AMO)，以程式設計方式來建立巢狀資料表，或使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的資料採礦精靈和資料採礦設計師來建立巢狀資料表。  
  
## <a name="using-nested-table-columns-in-a-mining-model"></a>在採礦模型中使用巢狀資料表資料行  
 在案例資料表中，索引鍵通常是客戶識別碼、產品名稱或數列中的日期，也就是能在資料表中唯一識別資料列的資料。 . 不過，在巢狀資料表中，索引鍵通常不是關聯式索引鍵 (或外部索引鍵)，而是代表您正在建模之屬性的資料行。  
  
 例如，如果案例資料表包含訂單，而巢狀資料表包含訂單中的項目，則您會想針對多個訂單的巢狀資料表所儲存項目之間的關聯性來建立模型 (這些訂單是儲存在案例資料表中)。 因此，雖然 **Items** 巢狀資料表會依照關聯式索引鍵 **OrderID** 聯結到 **Orders**案例資料表，但您不該使用 **OrderID** 作為巢狀資料表索引鍵。 而是應該選取 **Items** 資料行作為巢狀資料表索引鍵，因為該資料行包含您要建立模型的資料。 大多數的情況下，您都可以忽略採礦模型中的 **OrderID** 而不會發生問題，因為案例資料表和巢狀資料表之間的關聯性已藉由資料來源檢視定義而建立。  
  
 當您選擇資料行當做巢狀資料表索引鍵時，必須確定該資料行中的值對每個案例而言是唯一的。 例如，如果案例資料表代表客戶而巢狀資料表代表該客戶購買的項目，您就必須確定為每個客戶列出的項目不會超過一次。 如果客戶購買同一項目超過一次，則您可以建立不同的檢視，以提供資料行來彙總每項唯一產品的購買次數。  
  
 如何處理巢狀資料表中的重複值，是根據您建立的採礦模型以及要解決的商務問題而定。 在某些情況下，您可能並不在意客戶購買特定產品的次數，而只想檢查是否至少有一次購買的記錄； 在其他情況下，購買的數量及順序則可能很重要。  
  
 如果項目的順序很重要，則可能需要其他的資料行來代表順序。 使用時序叢集演算法來建立模型時，必須選擇其他的 *key sequence* 資料行來代表項目的順序。 Key Sequence 資料行是特殊種類的巢狀索引鍵，只會用於時序叢集模型且需要唯一的數值資料類型。 例如，整數和日期這兩者都可當做 Key Sequence 資料行，但所有的時序值都必須是唯一的。 除了 Key Sequence 資料行之外，時序叢集模型也擁有巢狀資料表索引鍵，用於代表要建立模型的屬性 (例如已購買的產品等)。  
  
### <a name="using-non-key-nested-columns-from-a-nested-table"></a>從巢狀資料表使用非索引鍵巢狀資料行  
 在您定義案例資料表及巢狀資料表之間的聯結，並選擇含有有趣及唯一的屬性 (要當做巢狀資料表索引鍵) 的資料行後，就可以包含巢狀資料表的其他資料行當做模型的輸出。 巢狀資料表的所有資料行都可用於輸出、預測及輸出，或僅用於預測。  
  
 例如，如果巢狀資料表包含資料行 **Product**、 **ProductQuantity**和 **ProductPrice**，您可以選擇 **Product** 作為巢狀資料表索引鍵，但對採礦結構加入 **ProductQuantity** 當作輸出。  
  
## <a name="filtering-nested-table-data"></a>篩選巢狀資料表資料  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您可以在用於定型或測試資料採礦模型的資料上建立篩選。 可以使用篩選器，會影響模型的撰寫或測試模型的案例子集上。 篩選也可以套用到巢狀資料表。 不過，巢狀資料表可使用的語法具有限制。  
  
 通常當您將篩選套用至巢狀資料表時，也是在測試屬性是否存在。 例如，您可以套用篩選，限制模型中所用的案例只能是在巢狀資料表中具有指定值的案例。 或者，也可以將模型中使用的案例限制為尚未購買過特定項目的客戶。  
  
 在巢狀資料表上建立篩選時，也可以使用大於或小於等運算子。 例如，您可以將模型中使用的案例限制為至少購買過 n 個目標產品的客戶。 對巢狀資料表屬性進行篩選的能力，可為模型的自訂提供極大的彈性。  
  
 如需如何建立及使用模型篩選的詳細資訊，請參閱[採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦結構 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
