---
title: 多維度模型中的檢視方塊 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e5e8a1748e54ea08b124b1db1b6048fce456b2f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="perspectives-in-multidimensional-models"></a>多維度模型中的檢視方塊
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  檢視方塊是針對特定應用程式或使用者的群組所建立之 Cube 的子集。 Cube 本身是預設檢視方塊。 檢視方塊會以 Cube 的形式向用戶端公開。 檢視方塊在使用者檢視時，會顯示成另一個 Cube 的樣子。 透過在檢視方塊中回寫，對 Cube 資料所做的任何變更，都是對原始 Cube 的變更。 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中之檢視的詳細資訊，請參閱[檢視方塊](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)。  
  
 使用 Cube 設計師中的 [檢視方塊] 索引標籤，即可建立或修改 Cube 中的檢視方塊。 [檢視方塊] 索引標籤的第一個資料行是 [Cube 物件] 資料行，會列出 Cube 中的所有物件。 這會對應到 Cube 的預設檢視方塊，也就是 Cube 本身。  
  
## <a name="creating-or-deleting-perspectives"></a>建立或刪除檢視方塊  
 您可以按一下 [Cube] 功能表上的 [新增檢視方塊]，將檢視方塊加入 [檢視方塊] 索引標籤。 您也可以按一下工具列上的 [新增檢視方塊] 按鈕，或者以滑鼠右鍵按一下窗格中的任何位置，然後按一下捷徑功能表上的 [新增檢視方塊]。 您可以將任意數量的檢視方塊加入至 Cube。  
  
 若要移除檢視方塊，請先按一下要刪除之檢視方塊的資料行裡任一個資料格。 然後，在 [Cube] 功能表上，按一下 [刪除檢視方塊]。 您也可以按一下工具列上的 [刪除檢視方塊] 按鈕，或者以滑鼠右鍵按一下要刪除之檢視方塊中的任一個資料格，然後按一下捷徑功能表上的 [刪除檢視方塊]。  
  
## <a name="renaming-perspectives"></a>重新命名檢視方塊  
 每個檢視方塊的第一個資料列會顯示它的名稱。 您建立檢視方塊時，初始的名稱為 Perspective (如果已經有名為 Perspective 的檢視方塊，則會在後面加上序號，從 1 開始)。 您可以按一下名稱，來編輯檢視方塊。  
  
## <a name="hiding-objects-from-a-perspective"></a>隱藏檢視方塊中的物件  
 若要隱藏檢視方塊中的物件，請清除資料列中的核取方塊，該資料列會對應到檢視方塊之資料行中的物件。 可以在檢視方塊中隱藏的 Cube 物件如下：  
  
-   量值群組  
  
-   量值  
  
-   維度  
  
-   階層  
  
-   命名集  
  
-   KPI  
  
-   動作  
  
-   導出成員  
  
 若要檢視任何物件，請展開 [Cube 物件] 之下，任何物件類型的類別目錄 ([量值群組]、[維度]、[KPI]、[計算] 或 [動作])。 若要檢視維度中的階層或屬性，請先展開維度，然後展開 [階層] 或 [屬性] 資料列。 若要檢視量值群組中的量值，請展開量值群組。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 cube](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
