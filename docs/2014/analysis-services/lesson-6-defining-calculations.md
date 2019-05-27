---
title: 第 6 課：定義計算 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e0a1e354-e879-4eb8-bb2b-6c3809e32cb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d8312019c5deeebb93185609433ae7e4925e3da
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078384"
---
# <a name="lesson-6-defining-calculations"></a>第 6 課：定義計算
  在這一課中，您要學習定義計算，它們是多維度運算式 (MDX) 運算式或指令碼。 計算可讓您定義導出成員、命名集，以及執行其他指令碼命令，以便擴充 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube 的功能。 例如，您可以執行指令碼命令，先定義 Subcube，然後再將計算指派給 Subcube 中的資料格。  
  
 當您在 Cube 設計師定義新的計算時，這些計算會加入至 Cube 設計師之 [計算] 索引標籤的 [指令碼組合管理] 窗格，而特定計算類型的欄位則是顯示在 [計算運算式] 窗格的計算表單中。 計算是以它們列示在 [指令碼組合管理] 窗格的順序來執行的。 您可以用滑鼠右鍵按一下特定的計算，然後選取 [上移] 或 [下移]；或者按一下特定的計算，然後在 [計算] 索引標籤的工具列上，按一下 [上移] 或 [下移] 圖示，重新排列計算。  
  
 您可以在 [計算] 索引標籤上，加入新的計算，以及在 [計算運算式] 窗格的下列檢視中，檢視或編輯現有的計算：  
  
-   表單檢視。 這份檢視所顯示的，是單一命令的運算式和屬性，以圖形格式表示。 當您編輯 MDX 指令碼時，運算式方塊會幫您填寫表單檢視。  
  
-   指令碼檢視。 這份檢視會以程式碼編輯器顯示所有的計算指令碼，讓您輕鬆變更計算指令碼。 如果 [計算運算式] 窗格是在指令碼檢視中，[指令碼組合管理] 就會隱藏起來。 指令碼檢視會提供色彩編碼、尋找相符括號、自動完成以及 MDX 程式碼區域。 您可以展開或收合 MDX 程式碼區域，讓編輯作業更加容易。  
  
 若要在 [計算運算式] 窗格中的這兩份檢視之間切換，請在 [計算] 索引標籤的工具列上，按一下 [表單檢視] 或 [指令碼檢視]。  
  
> [!NOTE]  
>  如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在任何計算中發現語法錯誤，就不會顯示表單檢視，除非指令碼檢視將錯誤更正。  
  
 您也可以利用商業智慧精靈，在 Cube 加入特定的計算。 例如，您可以利用這個精靈，將時間智慧加入 Cube 中，也就是說，針對與時間有關的計算 (例如，某週期至今、移動平均或循環週期成長率) 來定義導出成員。 如需詳細資訊，請參閱[使用商業智慧精靈定義時間智慧計算](multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)。  
  
> [!IMPORTANT]  
>  在 [計算] 索引標籤上，計算指令碼是以 CALCULATE 命令開頭。 CALCULATE 命令會控制 Cube 中的資料格彙總，不過，只有在您想要手動指定 Cube 資料格的彙總方式時，才編輯這個命令。  
  
 如需詳細資訊，請參閱 [計算](multidimensional-models-olap-logical-cube-objects/calculations.md)和 [多維度模型中的計算](multidimensional-models/calculations-in-multidimensional-models.md)。  
  
> [!NOTE]  
>  此教學課程中，所有課程已完成的專案都可在線上取得。 您可以從先前的課程中使用已完成的專案做為起點，向前跳到任何課程。 [按一下這裡](https://go.microsoft.com/fwlink/?LinkID=221866) ，下載此教學課程隨附的範例專案。  
  
 這一課包含下列工作：  
  
 [定義導出成員](../analysis-services/lesson-6-1-defining-calculated-members.md)  
 在這項工作中，您要學習定義導出成員。  
  
 [定義命名集](../analysis-services/lesson-6-2-defining-named-sets.md)  
 在這項工作中，您要學習定義命名集。  
  
## <a name="next-lesson"></a>下一課  
 [第 7 課：定義關鍵效能指標&#40;Kpi&#41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 教學課程案例](../analysis-services/analysis-services-tutorial-scenario.md)   
 [多維度模型化&#40;Adventure Works 教學課程&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)   
 [建立命名的集](multidimensional-models/create-named-sets.md)   
 [建立導出成員](multidimensional-models/create-calculated-members.md)  
  
  
