---
title: "將採礦模型加入結構 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], creating
- mining models [Analysis Services], creating
- mining models [Analysis Services], modifying
ms.assetid: a175daa5-58ea-474c-a82f-9648c5155dc8
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 42ae87b14d6ddff90b78bb3c23a7d536750d8317
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="add-mining-models-to-a-structure-analysis-services---data-mining"></a>將採礦模型加入至結構 (Analysis Services - 資料採礦)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
採礦結構是為了支援多個採礦模型。 因此在您完成此精靈之後，您可以開啟此結構，並加入新的採礦模型。 每當您建立模型時，您都可以使用不同的演算法、變更參數，或是將篩選套用到不同的資料子集。  
  
## <a name="adding-new-mining-models"></a>加入新的採礦模型  
 當您使用資料採礦精靈建立新的採礦模型時，預設一定要先建立採礦結構。 然後此精靈會提供您將初始採礦模型加入至結構中的選項。 不過，您不需要立刻建立模型。 如果您只建立結構，則不需要決定要使用哪個資料行做為可預測屬性，或者如何在特定模型中使用資料， 只需要設定將來要用的一般資料結構，稍後您可以使用 [資料採礦設計師](../../analysis-services/data-mining/data-mining-designer.md) 來加入以該結構為基礎的新採礦模型。  
  
> [!NOTE]  
>  在 DMX 中，CREATE MINING MODEL 陳述式會從採礦模型開始。 也就是說，您定義所要的採礦模型，然後 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會自動產生基礎結構。 稍後您可以使用 ALTER STRUCTURE... 陳述式繼續在該結構中加入新的採礦模型。 ADD MODEL 陳述式。  
  
## <a name="choosing-an-algorithm"></a>選擇演算法  
 當您將新的模型加入至現有結構時，您應該做的第一件事就是選取該模型中所要使用的資料採礦演算法。 選擇演算法非常重要，因為每一個演算法都會執行不同類型的分析，而且有不同的需求。  
  
 當您選取與資料不相容的演算法時，您會得到警告。 在某些情況下，您可能需要忽略此演算法所無法處理的資料行。 在其他案例中，此演算法會自動為您進行調整。 例如，如果您的結構包含數值資料，而且此演算法只能處理離散值，它會為您將數值分組為若干離散範圍。 在某些情況下，您可能需要先選擇索引鍵或可預測的屬性來手動修正資料。  
  
 當您建立新的模型時，您不需要變更演算法。 通常您可以使用相同的演算法，但是篩選資料或變更參數 (例如群集方法或項目集大小下限) 來得到非常不同的結果。 我們建議您試驗多個模型，以查看哪些參數會產生最佳的結果。  
  
 請注意，所有新的模型在使用之前都必須經過處理。  
  
## <a name="specifying-the-usage-of-columns-in-a-new-mining-model"></a>在新的採礦模型中指定使用資料行  
 當您將新的採礦模型加入至現有的採礦結構時，您必須指定此模型應該如何使用每一個資料行。 根據您為模型選擇的演算法類型而定，預設可能會進行某些選擇。 如果您不指定資料行的使用類型，採礦結構將不會包含此資料行。 不過，資料行中的資料依然可用於鑽研 (如果模型支援的話)。  
  
 採礦結構中由模型所使用的資料行 (如果未設定為 [忽略]) 必須為索引鍵、輸入資料行、可預測的資料行，或是值也會當做模型輸入的可預測資料行。  
  
-   索引鍵資料行包含資料表中每一個資料列的唯一識別碼。 某些採礦模型 (例如以時序群集或時間序列演算法為根據的模型) 可以包含多個索引鍵資料行。 不過，這些多個索引鍵並非具有關聯性意義的複合索引鍵，而是必須選取以提供時間序列和時序叢集分析支援的索引鍵。  
  
-   輸入資料行提供進行預測所根據的資訊。 [資料採礦精靈] 會提供 [建議] 功能，在選取可預測資料行時會啟用此功能。 如果您按一下這個按鈕，此精靈將會取樣可預測的值，並判斷結構中的哪些其他資料行會成為良好的變數。 它會拒絕含有許多唯一值的索引鍵資料行或其他資料行，並建議出現的資料行必須與結果相互關聯。  
  
     當資料集包含的資料行實際上比您建立採礦模型所需的資料行更多時，這項功能就會特別實用。 [建議] 功能會計算數值分數，從 0 到 1，描述資料集內的每一個資料行和可預測資料行之間的關聯性。 這項功能會依據此分數，建議用來作為採礦模型輸入的資料行。 如果使用 [建議] 功能，您可以使用建議的資料行、修改選取範圍以符合您的需求，或忽略建議。  
  
-   可預測資料行包含您嘗試在採礦模型中預測的資訊。 您可選取多個資料行當做可預測的屬性。 群集模型是例外狀況，因為可預測的模型為選擇性。  
  
     根據模型類型而定，可預測的資料行可能必須是特定的資料類型：例如，線性迴歸模型需要數值資料行當做預測值；貝氏機率分類演算法則需要離散值 (而且所有輸入也必須離散)。  
  
## <a name="specifying-column-content"></a>指定資料行內容  
 對某些資料行而言，您可能也需要指定「資料行內容」。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦中，每個資料行的內容類型屬性都會告訴演算法它該如何處理該資料行中的資料。 例如，如果資料有「收入」資料行，則您必須將內容類型設定為「連續」，指定該資料行包含連續的數字。 不過，您也可以將內容類型設定為「離散」並選擇性地指定確切的值區數，以指定將「收入」資料行中的數字分組為值區。 您可以建立以不同方式處理資料行的不同模型：例如，您可以嘗試將客戶區分為三個年齡群組值區的模型，也可以使用另一個將客戶區分為 10 個年齡群組值區的模型。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構 &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [建立關聯式採礦結構](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [採礦模型屬性](../../analysis-services/data-mining/mining-model-properties.md)   
 [採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)  
  
  
