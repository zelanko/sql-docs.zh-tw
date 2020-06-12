---
title: 在資料來源視圖設計工具中使用圖表（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.diagramorganizerpane.f1
- sql12.asvs.dsvdesigner.findtable.f1
- sql12.asvs.dsvdesigner.diagrampane.f1
helpviewer_keywords:
- data source views [Analysis Services], diagrams
- diagrams [Analysis Services]
ms.assetid: 491fdd22-2326-4f27-a0dd-0a02faae3fd8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 006f1090faed746737a89041593222d95637d387
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541200"
---
# <a name="work-with-diagrams-in-data-source-view-designer-analysis-services"></a>在資料來源檢視設計工具中使用圖表 (Analysis Services)
  資料來源檢視 (DSV) 圖表是 DSV 中物件的視覺表示法。 您可以使用圖表以互動方式加入、隱藏、刪除或修改特定物件。 您也可以在相同的 DSV 中建立多個圖表，將注意集中在物件子集。  
  
 若要變更圖表窗格中出現的圖表區域，請按一下窗格右下角之四個方向的箭頭，然後將選擇方塊拖曳至縮圖圖表上方，直到選取要出現在圖表窗格中的區域為止。  
  
 這個主題包括下列各節：  
  
 [加入圖表](#bkmk_add)  
  
 [編輯或刪除圖表](#bkmk_edit)  
  
 [在圖表中尋找資料表](#bkmk_findtables)  
  
 [排列圖表中的物件](#bkmk_arrangeobjects)  
  
 [保留物件相片順序](#bkmk_preserve)  
  
##  <a name="add-a-diagram"></a><a name="bkmk_add"></a>新增圖表  
 DSV 圖表會在您建立 DSV 時自動建立。 DSV 存在之後，即可建立其他圖表、移除圖表或隱藏特定物件，以建立更容易管理的 DSV 表示法。  
  
 若要建立新圖表，請以滑鼠右鍵按一下 [圖表組合管理]**** 窗格中的任何位置，然後按一下 [新增圖表]****。  
  
 當您一開始在 Analysis Services 專案中定義資料來源視圖（DSV）時，加入至資料來源視圖的所有資料表和 views 都會加入至 \<All Tables> 圖表中。 這個圖表會出現在資料來源檢視設計師的 [圖表組合管理] 窗格內，而這個圖表中的資料表 (以及其資料行和關聯性) 會列在 [資料表] 窗格內，而且這個圖表中的資料表 (以及其資料行和關聯性) 會以圖形方式顯示在結構描述窗格內。 不過，當您在圖表中加入資料表、視圖和名稱查詢時 \<All Tables> ，此圖表中的物件數量非常難以視覺化關聯性，尤其是將多個事實資料表加入至圖表，而維度資料表與多個事實資料表相關。  
  
 當您只想要在資料來源檢視中檢視資料表的子集時，如果要減少視覺上的混亂情形，您可以在此資料來源檢視中定義由資料表、檢視和具名查詢的選定子集所組成的子圖表 (就稱為圖表)。 您可以使用圖表，根據商務或方案需求，將資料來源檢視中的項目分組。  
  
 基於商業用途，您可以將相關資料表和具名查詢分組在不同的圖表中，讓人更容易了解包含許多資料表、檢視和具名查詢的資料來源檢視。 相同的資料表或命名的查詢可以包含在多個圖表中，但 \<All Tables> 圖表除外。 在 \<All Tables> 圖表中，資料來源視圖中所包含的所有物件只會顯示一次。  
  
##  <a name="edit-or-delete-a-diagram"></a><a name="bkmk_edit"></a>編輯或刪除圖表  
 使用圖表時，請特別注意用於加入及移除物件的命令。 例如，從圖表中刪除物件會從 DSV 中刪除相同物件。 如果您只想將其從圖表中刪除，請改用 **[隱藏資料表]** 。  
  
 ![圖表工作空間的螢幕擷取畫面，以滑鼠右鍵按一下功能表](../media/ssas-olapdsv-diagram.gif "圖表工作空間的螢幕擷取畫面，以滑鼠右鍵按一下功能表")  
  
 雖然您可以個別隱藏物件，但是使用 [顯示相關資料表] 命令重新顯示物件時，會將所有相關物件傳回圖表。 若要控制傳回工作空間的物件，請改為從 [資料表] 窗格中拖曳物件。  
  
##  <a name="find-tables-in-a-diagram"></a><a name="bkmk_findtables"></a>在圖表中尋找資料表  
 如果結構描述很大，則在 **[圖表]** 窗格中捲動至特定資料表可能會有困難。 然而，下列工具可讓您輕鬆地尋找圖表中的資料表。  
  
-   在 **[資料表]** 窗格中捲動資料表清單。  
  
     若要將資料表包含在目前顯示的圖表中，請將資料表從 **[資料表]** 窗格拖曳到圖表窗格。  
  
     若要將圖表中已包含的資料表置中顯示，請在 **[資料表]** 窗格中選取資料表。  
  
-   **圖表**窗格中的資料表定位器-資料表定位器是四向箭號圖示，位於 [**圖表**] 窗格右下角垂直和水準捲軸的交集處。 它會開啟 [圖表] 窗格中目前圖表的縮圖表示。 您可以使用此縮圖，將 [圖表] 窗格中的檢視變更至圖表的任何位置。  
  
-   使用 [**尋找資料表**] 對話方塊-以滑鼠右鍵按一下 [圖表] 窗格中的 [開啟區域]，然後按一下 [**尋找資料表**]。 或者，按一下工具列上的 **[尋找資料表]** 命令或 **[資料來源檢視]** 功能表。  
  
     您可以在 [篩選] 方塊中輸入字串和萬用字元，來檢視圖表中的資料表子集。  
  
##  <a name="arrange-objects-in-a-diagram"></a><a name="bkmk_arrangeobjects"></a>排列圖表中的物件  
 雖然資料來源檢視設計工具可以定義多個圖表，讓 DSV 更容易了解，但包含太多資料表的圖表就很難閱讀，且手動重新排列資料表配置又是一件耗時的工作。 資料來源檢視設計師可以根據目前圖表中資料表之間的關聯性，使用矩形或對角線配置，來自動重新排列目前圖表中的資料表。  
  
-   在矩形配置中，關聯性線條是在資料表之間而非資料行之間繪製。 關聯性線條會水平及垂直地繪製在資料表之間。  
  
-   在對角線配置中，關聯性線條會盡可能直接繪製在資料表的相關資料行之間。 多個資料行的關聯性會附加至資料表中的第一個相關資料行。 如果看不到資料表中的資料行，則線條會繪製在資料表頂端。  
  
##  <a name="preserve-object-arrangement"></a><a name="bkmk_preserve"></a>保留物件相片順序  
 依照所要的方式手動排列資料表之後，將更多資料表加入至圖表可能會造成圖表重新整理，而移除您對物件配置的最近修改。  
  
 當您加入資料表時，導致 [圖表組合管理] 移動其他資料表以容納新資料表，可能會發生這種行為。 然後它會重新繪製圖表，確保所有資料表和連接線正確表示。 此時，對特定物件位置的所有手動調整可能會遺失。  
  
 若要避免這個問題，請先加入所有資料表，然後進行最後調整。 當您稍後重新開啟圖表時，物件現在應該會保留其圖表中的位置。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源視圖](data-source-views-in-multidimensional-models.md)   
 [資料來源檢視設計工具 &#40;Analysis Services - 多維度資料&#41;](../data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
