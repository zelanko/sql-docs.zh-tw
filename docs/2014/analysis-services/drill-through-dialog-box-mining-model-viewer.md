---
title: 鑽研對話方塊 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 331ab6da3e2e244f3a0413d80006ceeb907704f4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151469"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>鑽研對話方塊 (採礦模型檢視器)
  當您使用「資料採礦設計師」的 **[採礦模型檢視器]** 索引標籤檢視採礦模型時，假設該模型已啟用鑽研，您就可以鑽研到案例資料的相關詳細資料。 此外，如果基礎採礦結構已啟用鑽研，您也可以看到採礦結構中的資料行 (即使這些資料行不包含在採礦模型中)。 在資料行清單中，結構資料行的前面會加上 "Structure." 標籤。  
  
> [!NOTE]  
>  您無法針對現有的採礦結構啟用鑽研。 而必須重新建立採礦結構，然後在建立程序期間啟用鑽研。  
  
 如需如何從每個支援鑽研的採礦模型檢視器存取案例資料的詳細資訊**請參閱 <<c2>**   [鑽研到案例資料採礦模型的](data-mining/drill-through-to-case-data-from-a-mining-model.md)。  
  
## <a name="options"></a>選項。  
 **案例分類為**  
 顯示所選節點中所包含之規則、項目集和叢集的定義。  
  
 **資料行清單**  
 顯示模型中的資料行，後面接著結構資料行。  
  
 **注意** —只有在採礦結構上啟用鑽研，而且選取 **[模型和結構資料行]** 選項時，才會顯示結構資料行。 此外，您必須同時擁有採礦模型和採礦結構的鑽研權限，才能檢視資料行。  
  
 不包含在模型中的結構資料行顯示為**結構。\<資料行名稱 >**。  
  
> [!NOTE]  
>  您可以以滑鼠右鍵按一下詳細資料方格中的任意位置，然後選取 [全部複製]，以 Tab 分隔的格式，將鑽研資料複製到剪貼簿。 複製的資料僅包含案例資料，而不包含節點定義。  
  
 **播放**  
 按一下綠色箭頭按鈕可重新整理資料。  
  
## <a name="see-also"></a>另請參閱  
 [鑽研查詢&#40;資料採礦&#41;](data-mining/drillthrough-queries-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [採礦模型檢視器工作和操作說明](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
