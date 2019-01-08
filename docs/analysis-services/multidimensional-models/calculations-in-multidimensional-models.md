---
title: 多維度模型中的計算 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c72d43c95013074051356c690ac2d7abf0a575e0
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2018
ms.locfileid: "52983989"
---
# <a name="calculations-in-multidimensional-models"></a>多維度模型中的計算
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  使用 [Cube 設計師] 的 [計算] 索引標籤來建立導出成員、命名集，和其他多維度運算式 (MDX) 計算。  
  
 [計算] 索引標籤具有下列三個窗格：  
  
-   [指令碼組合管理] 窗格列出 Cube 中的計算。 使用此窗格來建立、組織和選取計算以進行編輯。  
  
-   [計算工具] 窗格提供用來建立計算的中繼資料、函數和範本。  
  
-   [計算運算式] 窗格支援表單檢視與指令碼檢視。  
  
  
## <a name="creating-a-new-calculation"></a>建立新的計算  
 若要建立新的計算，請在 [Cube 設計師] 之 [計算] 索引標籤的 [Cube] 功能表上，依照您要建立的計算類型，按一下 [新增導出成員]、[新增命名集] 或 [新增指令碼命令]。 您也可以在工具列上按一下任何對應的按鈕，或以滑鼠右鍵按一下 [指令碼組合管理] 窗格中的任何位置，然後按一下快速鍵功能表上的其中一個命令。 此動作會將新計算加入 [指令碼組合管理] 窗格，並在 [計算運算式] 窗格的計算表單中顯示其欄位。 如果您建立新的指令碼，此動作會在 [計算運算式] 窗格中開啟 [指令碼] 檢視。 如需建立三種計算類型的詳細資訊，請參閱 [建立導出成員](../../analysis-services/multidimensional-models/create-calculated-members.md)、 [建立命名集](../../analysis-services/multidimensional-models/create-named-sets.md)和 [定義指派和其他指令碼命令](../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)。  
  
## <a name="editing-scripts"></a>編輯指令碼  
 在 [計算] 索引標籤的 [計算運算式] 窗格中編輯指令碼。[計算運算式] 窗格有兩個檢視，[指令碼] 檢視和 [表單] 檢視。 [表單] 檢視會顯示單一命令的運算式與屬性。 編輯 MDX 指令碼時，運算式方塊會填滿整個 [表單] 檢視。  
  
 [指令碼] 檢視提供用來編輯指令碼的程式碼編輯器。 當 [計算運算式] 窗格處於 [指令碼] 檢視時，會隱藏 [指令碼組合管理] 窗格。 指令碼檢視會提供色彩編碼、尋找相符括號、自動完成以及 MDX 程式碼區域。 MDX 程式碼區域可以摺疊或展開，以利編輯。  
  
 您可以按一下 [Cube] 功能表，指向 [顯示計算於]，然後按一下 [指令碼] 或 [表單]，即可在 [表單] 檢視與 [指令碼] 檢視間切換。 您也可以在工具列上按一下 [表單檢視] 或 [指令碼檢視]。  
  
## <a name="changing-solve-order"></a>變更求解順序  
 系統會以 [指令碼組合管理] 窗格中列出的順序來解決計算。 您可以滑鼠右鍵按一下任何計算，然後按一下快速鍵功能表上的 [上移] 或 [下移]，重新將計算排序。 您也可以按一下計算，然後在工具列按一下 [上移] 或 [下移] 按鈕。  
  
 您可以針對導出資料格與導出成員，以手動方式覆寫此順序。 如需行程順序和求解順序的詳細資訊，請參閱[了解行程順序和求解順序 &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
## <a name="deleting-a-calculation"></a>刪除計算  
 若要刪除現有的計算，請在 [計算] 索引標籤上，於 [指令碼組合管理] 窗格中，選取要刪除的計算，然後在 [編輯] 功能表上按一下 [刪除]，或在工具列上按一下**刪除**圖示。 您也可以在 [指令碼組合管理] 窗格中以滑鼠右鍵按一下計算，然後從快速鍵功能表中選取 [刪除]。  
  
  
