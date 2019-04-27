---
title: 建立輪詢查詢對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.createpollingquerydialog.f1
ms.assetid: 0f2902b5-796a-4eb0-be03-01514dc01b9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b58e73b7757e8288ff90f462be1868cb60e3af5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679726"
---
# <a name="create-polling-query-dialog-box-analysis-services---multidimensional-data"></a>建立輪詢查詢對話方塊 (Analysis Services - 多維度資料)
  使用 **中的** [建立輪詢查詢] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 對話方塊，即可在 **[儲存選項]** 對話方塊的 **[通知]** 索引標籤上建立輪詢查詢。 輪詢查詢通常為單一查詢，可傳回一個值，供 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來判斷資料表或其他關聯式物件是否已變更。 您可以在 [儲存選項] 對話方塊之 [通知] 索引標籤上的 [排程輪詢] 選項中，於方格的 [輪詢查詢] 資料行上，按一下省略符號按鈕 (**...**)，以顯示 [建立輪詢查詢] 對話方塊。 如需 [儲存選項] 對話方塊之 [通知] 索引標籤的詳細資訊，請參閱 [Notifications &#40;Storage Options Dialog Box&#41; &#40;Analysis Services - Multidimensional Data&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md) (通知 ([儲存選項] 對話方塊) (Analysis Services - 多維度資料))。  
  
 輪詢查詢應該傳回的值類型，會視所查詢資料表之物件的多維度 OLAP (MOLAP) 快取所計畫的更新類型而定：  
  
-   如果 **[儲存選項]** 對話方塊的 **[通知]** 索引標籤上，未選取 **[啟用累加式更新]** ，則在排程輪詢期間偵測到變更時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會完全更新物件的 MOLAP 快取。 使用的輪詢查詢應該會判斷在上次輪詢期間之後，是否有記錄加入至資料表。  
  
-   如果在 **[儲存選項]** 對話方塊的 **[通知]** 索引標籤上，選取 **[啟用累加式更新]** ，則在排程輪詢期間偵測到變更時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會累加地更新物件的 MOLAP 快取。 使用的輪詢查詢應該會判斷資料表的最後一筆記錄。  
  
 例如，您可以使用下列輪詢查詢，對 [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] 範例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中的 Customer 維度，提供完整或累加式更新：  
  
|更新類型|[排程輪詢]|  
|-----------------|-------------------|  
|完整更新|`SELECT`<br /><br /> `COUNT(*) AS TotalCount`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|累加式更新|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
  
 如需排程輪詢通知之完全和累加式更新的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
 輸入的查詢必須是基礎提供者的有效查詢命令。 此查詢會由基礎提供者進行驗證，以及識別傳回的資料行。 對話方塊可呈現兩種檢視：  
  
-   Visual Database Tools (VDT) 查詢產生器  
  
     對於所有使用者，VDT 查詢產生器的檢視所提供的使用者介面工具集，能夠以視覺化方式建構及測試 SQL 查詢。  
  
-   一般查詢產生器  
  
     對於進階使用者，一般查詢產生器檢視提供更簡單、更直接的使用者介面，可以用來建構及測試 SQL 查詢。  
  
## <a name="options"></a>選項。  
 **資料來源**  
 指定查詢的資料來源。  
  
 **查詢定義**  
 視選取的檢視而定，查詢定義會提供工具列和窗格，以定義及測試查詢。  
  
 **工具列**  
 使用工具列即可管理資料集、選取要顯示的窗格和控制各種查詢功能。  
  
|值|描述|  
|-----------|-----------------|  
|**切換到一般查詢產生器**|選取即可只顯示一般查詢產生器檢視可用的選項。 僅會顯示下列選項：<br /><br /> **SQL 窗格**<br /><br /> **結果窗格**<br /><br /> **工具列**，只包含 **[切換到 VDT 查詢產生器]** 和 **[執行]**<br /><br /> <br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
|**切換到 VDT 查詢產生器**|選取即可顯示 Visual Database Tools (VDT) 查詢產生器檢視可用的所有選項。<br /><br /> 注意:會顯示此選項，只有當**切換到一般查詢產生器**已選取。|  
|**顯示/隱藏圖表窗格**|顯示或隱藏 **[圖表窗格]**。<br /><br /> 注意:會顯示此選項，只有當**切換到 VDT 查詢產生器**已選取。|  
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
  
  
