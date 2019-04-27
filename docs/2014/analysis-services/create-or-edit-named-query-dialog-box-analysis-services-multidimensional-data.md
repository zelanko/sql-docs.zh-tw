---
title: 建立或編輯具名的查詢對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createnamedquery.f1
helpviewer_keywords:
- Create Named Query dialog box
ms.assetid: 8e192ad6-a0b1-4e21-bb3f-087c93e62941
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc03192d0deae00b9ace6f70e72ced4883d26b1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679766"
---
# <a name="create-or-edit-named-query-dialog-box-analysis-services---multidimensional-data"></a>建立或編輯具名查詢對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [建立/編輯具名查詢] 對話方塊，即可建立或編輯 [資料來源檢視設計師] 中的具名查詢。 具名查詢可以當成資料表處理，並以此作為其他 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件的基礎。 您可以執行下列動作來顯示 [建立/編輯具名查詢] 對話方塊：  
  
-   在 [資料來源檢視設計師] 的 [工具列] 窗格上，按一下 [新增具名查詢]。  
  
-   以滑鼠右鍵按一下 [資料來源檢視設計師] 的 [圖表] 窗格，然後選取 [新增具名查詢]。  
  
-   在 [資料來源檢視設計師] 的 [圖表] 或 [資料表] 窗格中，以滑鼠右鍵按一下具名查詢的名稱，然後選取 [編輯具名查詢]。  
  
 輸入的查詢必須是基礎提供者的有效查詢命令。 此查詢會由基礎提供者進行驗證，以及識別傳回的資料行。 對話方塊可呈現兩種檢視：  
  
-   Visual Database Tools (VDT) 查詢產生器  
  
     對於所有使用者，VDT 查詢產生器的檢視所提供的使用者介面工具集，能夠以視覺化方式建構及測試 SQL 查詢。  
  
-   一般查詢產生器  
  
     對於進階使用者，一般查詢產生器檢視提供更簡單、更直接的使用者介面，可以用來建構及測試 SQL 查詢。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入查詢的名稱。  
  
 **說明**  
 鍵入查詢的選用性描述。  
  
 **資料來源**  
 指定查詢的資料來源。  
  
 **查詢定義**  
 視選取的檢視而定，查詢定義會提供工具列和窗格，以定義及測試查詢。  
  
 **工具列**  
 使用工具列即可管理資料集、選取要顯示的窗格和控制各種查詢功能。  
  
|值|描述|  
|-----------|-----------------|  
|**切換到一般查詢產生器**|選取即可只顯示一般查詢產生器檢視可用的選項。 僅會顯示下列選項：<br />**SQL 窗格**<br />**結果窗格**<br />**工具列**，只包含 **[切換到 VDT 查詢產生器]** 和 **[執行]**<br /><br /> <br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**切換到 VDT 查詢產生器**|選取即可顯示 Visual Database Tools (VDT) 查詢產生器檢視可用的所有選項。<br /><br /> 注意:會顯示此選項，只有當**切換到一般查詢產生器**已選取。|  
|**顯示/隱藏圖表窗格**|顯示或隱藏 **[圖表窗格]**。<br /><br /> **注意**：唯有選取 [切換到 VDT 查詢產生器] 才會顯示此選項。|  
|**顯示/隱藏方格窗格**|顯示或隱藏 **[方格窗格]**。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**顯示/隱藏 SQL 窗格**|顯示或隱藏 **[SQL 窗格]**。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**顯示/隱藏結果窗格**|顯示或隱藏 **[結果窗格]**。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**執行**|執行查詢。 結果會顯示在 **[結果窗格]** 中。|  
|**驗證 SQL**|驗證查詢中的 SQL 陳述式。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**遞增排序**|依遞增順序排序 **[方格窗格]** 中所選取資料行的輸出資料列。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**遞減排序**|依遞減順序排序在 **[方格窗格]** 中所選取資料行的輸出資料列。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**移除篩選**|如果適用的話，移除 **[方格窗格]** 中所選取資料列的排序準則。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**使用群組依據**|將群組功能加入查詢中。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**新增資料表**|顯示 **[加入資料表]** 對話方塊，將新的資料表或檢視加入查詢中。 如需 [加入資料表] 對話方塊的詳細資訊，請參閱[加入資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
  
 **圖表窗格**  
 以圖表顯示查詢所參考的物件。 此圖表顯示查詢所包括的資料表及其聯結方式。 選取或清除資料表之資料行旁邊的核取方塊，以便在查詢輸出中加入或移除。  
  
 當您在查詢中加入資料表時，對話方塊會依據資料表中的索引鍵，在資料表之間建立聯結。 若要加入聯結，請將欄位從一個資料表拖曳至另一個資料表的欄位。 若要管理聯結，請以滑鼠右鍵按一下聯結。  
  
 以滑鼠右鍵按一下 [圖表窗格]，即可加入或移除資料表、選取所有資料表以及顯示或隱藏窗格。  
  
> [!NOTE]  
>  [圖表窗格]、[方格窗格] 和 [SQL 窗格] 的內容會同步處理，因此一個窗格的變更會反映在其他兩個窗格中。  
  
> [!IMPORTANT]  
>  此對話方塊不支援變更查詢類型。  
  
 **方格窗格**  
 以方格的方式顯示查詢所參考的物件。 您可以使用此方格，在查詢中加入和移除資料行，以及變更每一個資料行的設定。  
  
> [!NOTE]  
>  [圖表窗格]、[方格窗格] 和 [SQL 窗格] 的內容會同步處理，因此一個窗格的變更會反映在其他兩個窗格中。  
  
 **SQL 窗格**  
 以 SQL 陳述式顯示查詢。 鍵入資料，以變更查詢的 SQL 陳述式。  
  
> [!NOTE]  
>  [圖表窗格]、[方格窗格] 和 [SQL 窗格] 的內容會同步處理，因此一個窗格的變更會反映在其他兩個窗格中。  
  
 **結果窗格**  
 按一下 [工具列] 窗格上的 [執行] 時，會顯示查詢的結果。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [在資料來源檢視中定義具名查詢 &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  
