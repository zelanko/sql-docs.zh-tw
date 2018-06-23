---
title: 建立處理查詢對話方塊 (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.createprocessingquerydialog.f1
ms.assetid: c133d624-f35e-486e-be9f-ceafd906f168
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 01633f8b8ce57d3b8953c1694a250cfdb9a64cc7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133825"
---
# <a name="create-processing-query-dialog-box-analysis-services---multidimensional-data"></a>建立處理查詢對話方塊 (Analysis Services - 多維度資料)
  使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [建立處理查詢] 對話方塊，即可在 [儲存選項] 對話方塊的 [通知] 索引標籤中建立處理查詢。 處理查詢是會傳回資料列集的查詢，資料列集內會包含與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 物件相關聯之資料表所做的變更，而且會是上一次輪詢資料表之後所做的變更，如此才能累加地更新該物件的多維度 OLAP (MOLAP) 快取。 Analysis Services 使用另一種查詢 (稱為輪詢查詢) 來輪詢與物件相關聯的資料表，並決定是否已變更該資料表。 完全更新物件的 MOLAP 快取時，不需要處理查詢。  
  
 通常，處理查詢是參數化的，且目前支援兩個參數：  
  
-   在先前的排程輪詢期間，輪詢查詢所傳回的單一值。  
  
-   在目前的排程輪詢期間，輪詢查詢所傳回的單一值。  
  
 例如，下表所列的查詢可用來累加地更新 Adventure Works DW 範例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案中的客戶維度。  
  
|查詢類型|查詢陳述式|  
|----------------|---------------------|  
|[排程輪詢]|`SELECT`<br /><br /> `MAX([CustomerKey]) AS LastCustomerKey`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`|  
|處理查詢|`SELECT`<br /><br /> `*`<br /><br /> `FROM`<br /><br /> `[dbo].[DimCustomer]`<br /><br /> `WHERE`<br /><br /> `(CustomerKey > COALESCE (@Param1, - 1))`<br /><br /> `AND (CustomerKey <= @Param2)`|  
  
 如需排程輪詢通知累加式更新的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
 在 [儲存選項] 對話方塊的 [通知] 索引標籤上，於 [排程輪詢] 選項之方格的 [正在處理查詢] 資料行上，按一下 [...]，即可顯示 [建立處理查詢] 對話方塊。 如需 [儲存選項] 對話方塊之 [通知] 索引標籤的詳細資訊，請參閱[通知 &#40;儲存選項對話方塊&#41; &#40;Analysis Services - 多維度資料&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)。  
  
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
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**切換到一般查詢產生器**|選取即可只顯示一般查詢產生器檢視可用的選項。 僅會顯示下列選項：<br /><br /> **SQL 窗格**<br /><br /> **結果窗格**<br /><br /> **工具列**，只包含 **[切換到 VDT 查詢產生器]** 和 **[執行]**<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**切換到 VDT 查詢產生器**|選取即可顯示 Visual Database Tools (VDT) 查詢產生器檢視可用的所有選項。<br /><br /> 注意：唯有選取 [切換到一般查詢產生器]  才會顯示此選項。|  
|**顯示/隱藏圖表窗格**|顯示或隱藏 **[圖表窗格]**。<br /><br /> **注意**：唯有選取 [切換到 VDT 查詢產生器] 才會顯示此選項。|  
|**顯示/隱藏方格窗格**|顯示或隱藏 **[方格窗格]**。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**顯示/隱藏 SQL 窗格**|顯示或隱藏 **[SQL 窗格]**。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**顯示/隱藏結果窗格**|顯示或隱藏 **[結果窗格]**。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**執行**|執行查詢。 結果會顯示在 **[結果窗格]** 中。|  
|**驗證 SQL**|驗證查詢中的 SQL 陳述式。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**遞增排序**|依遞增順序排序 **[方格窗格]** 中所選取資料行的輸出資料列。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**遞減排序**|依遞減順序排序在 **[方格窗格]** 中所選取資料行的輸出資料列。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**移除篩選**|如果適用的話，移除 **[方格窗格]** 中所選取資料列的排序準則。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**使用群組依據**|將群組功能加入查詢中。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
|**新增資料表**|顯示 **[加入資料表]** 對話方塊，將新的資料表或檢視加入查詢中。 如需 [加入資料表] 對話方塊的詳細資訊，請參閱[加入資料表對話方塊 &#40;Analysis Services - 多維度資料&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 注意：唯有選取 [切換到 VDT 查詢產生器]  才會顯示此選項。|  
  
 **圖表窗格**  
 以圖表顯示查詢所參考的物件。 此圖表顯示查詢所包括的資料表及其聯結方式。 選取或清除資料表之資料行旁邊的核取方塊，以便在查詢輸出中加入或移除。  
  
 當您在查詢中加入資料表時，對話方塊會依據資料表中的索引鍵，在資料表之間建立聯結。 若要加入聯結，請將欄位從一個資料表拖曳至另一個資料表的欄位。 若要管理聯結，請以滑鼠右鍵按一下聯結。  
  
 以滑鼠右鍵按一下 [圖表窗格]，即可加入或移除資料表、選取所有資料表以及顯示或隱藏窗格。  
  
> [!NOTE]  
>  [圖表窗格]、[方格窗格] 和 [SQL 窗格] 的內容會同步處理，因此一個窗格的變更會反映在其他兩個窗格中。  
  
> [!IMPORTANT]  
>  此對話方塊不支援變更查詢類型。  
  
 **在方格窗格**  
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
  
  