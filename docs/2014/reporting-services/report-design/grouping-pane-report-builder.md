---
title: 群組窗格 (報表產生器) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10033"
helpviewer_keywords:
- Grouping Pane dialog box
ms.assetid: 983ee5a4-944c-491e-8720-7cd9f3881961
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 88636af497e2049e6cb0925d5448df56dbeb98ba
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291790"
---
# <a name="grouping-pane-report-builder"></a>群組窗格 (報表產生器)
  [群組] 窗格會顯示目前所選 Tablix 資料區的資料列群組和資料行群組。 [群組] 窗格不適用於 [圖表] 或 [量測計] 資料區。 [群組] 窗格包含 [資料列群組] 窗格和 [資料行群組] 窗格。 [群組] 窗格有兩種模式：預設和進階。 預設模式會針對資料列和資料行群組，顯示動態成員的階層式檢視。 進階模式則會針對資料列和資料行群組，同時顯示動態和靜態成員。 群組是來自顯示於資料區域上之報表資料集的命名集資料。 群組會組織成包含靜態和動態成員的階層。 如需詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  如果看不到 [群組] 窗格，請在 [檢視] 索引標籤的 [顯示/隱藏] 群組中，按一下 [群組]。  
  
 資料列和資料行群組區域中的資料格可以是 Tablix 資料列或資料行群組的靜態或動態成員。 每個群組的靜態成員都會重複一次，而且通常包含標籤或總計。 每個群組執行個體的動態成員都會重複一次，而且通常包含群組運算式的唯一值。 當您在資料列群組區域或資料行群組區域中選取 Tablix 資料格時，就會在 [資料列群組] 或 [資料行群組] 窗格中選取對應的群組成員。 相反地，如果您在 [群組] 窗格中選取群組，就會在設計介面上選取與群組成員相關聯的對應資料格。 如需 Tablix 資料列和資料行群組區域的詳細資訊，請參閱 [Tablix 資料區的區域 &#40;報表產生器及 SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
 [群組] 窗格支援下列模式：  
  
-   **預設值：** 使用預設模式加入、編輯或刪除群組。 您可以從 [報表資料] 窗格拖曳欄位，並將這些欄位插入到群組階層中，藉以加入父群組、子群組和詳細資料群組。 若要加入相鄰群組，您必須使用 **[加入群組]** 快速鍵。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
-   **進階**： 使用 **[進階模式]** 檢視資料列和資料行群組的所有成員，並針對靜態成員設定屬性。 當您建立群組或加入總計時，會自動設定控制 Tablix 資料區域如何在每個報表頁面上轉譯資料列與資料行的屬性。 若要手動調整這些屬性，您必須針對 Tablix 成員設定這些屬性。 如需詳細資訊，請參閱 [控制報表頁面上的 Tablix 資料區顯示 &#40;報表產生器及 SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)。  
  
## <a name="default-mode"></a>預設模式  
 在預設模式下，[資料列群組] 窗格和 [資料行群組] 窗格會顯示所有父群組、子群組和相鄰群組的階層式檢視。 子群組會以縮排顯示在其父群組下。 相鄰群組會與其同層級群組顯示在相同的縮排層級上。 下圖顯示 Tablix 資料區與巢狀資料列群組，以及巢狀資料行和相鄰資料行群組。  
  
 ![Tablix、巢狀及相鄰的資料列和資料行群組](../media/rs-basictablixdesigngroupingpane.gif "Tablix、巢狀及相鄰的資料列和資料行群組")  
  
 [群組] 窗格會顯示對應的資料列和資料行群組。 在下圖中，以子類別目錄為基礎的群組已在 [資料列群組] 窗格中選取，而 [Subcat] 群組資料格則已在 Tablix 資料區中選取：  
  
 ![巢狀資料列和資料行群組的群組窗格](../media/rs-basictablixdesigngroupingpanedefaultview.gif "巢狀資料列和資料行群組的群組窗格")  
  
 在 [資料列群組] 窗格中，以子類別目錄為基礎之群組是以類別目錄為基礎之群組的子系。 在 [資料行群組] 窗格中，國家/地區群組是地理位置群組的子系。 年份群組和國家/地區群組則是相鄰的群組。  
  
 如需詳細資訊，請參閱 [Tablix 資料區資料格、資料列及資料行 &#40;報表產生器及 SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)。  
  
## <a name="advanced-mode"></a>[進階模式]  
 在進階模式下，[資料列群組] 窗格和 [資料行群組] 窗格會顯示所有群組的階層式檢視，包括靜態和動態成員。 當您選取成員時，[屬性] 窗格會顯示目前選取之 Tablix 成員的屬性。  
  
> [!NOTE]  
>  若要切換 [進階模式]，請以滑鼠右鍵按一下 [資料行群組] 窗格旁邊的向下箭頭，然後按一下 [進階模式]。  
  
 在大部分的情況下，控制靜態與動態群組資料列和群組資料行之顯示的屬性會在建立群組或加入總計時自動設定。 若要編輯預設值，您必須在 [資料列群組] 或 [資料行群組] 窗格中選取群組成員，然後在 [屬性] 視窗中變更屬性值。 同時會提供下列屬性：  
  
-   **FixedData**： 布林值。 用於外部資料列和資料行標頭。 在轉譯器 (例如 HTML) 中垂直捲動時凍結資料列群組區域，或在水平捲動時凍結資料行群組區域。  
  
-   **HideIfNoRows**： 布林值。 僅用於靜態成員。 如果有設定，則會忽略 Hidden 和 ToggleItem。 如果 Tablix 資料區不包含資料的資料列，則隱藏此成員。  
  
-   **KeepTogether**： 布林值。 指出要盡可能將整個 Tablix 成員和任何巢狀成員保持在單一頁面上。  
  
-   `KeepWithGroup`. 布林值。 僅用於靜態資料列成員。 在可能的情況下，保留此資料列與之前或之後的同層級動態成員 (如果未隱藏)。 若要將資料列標頭與其相關聯的群組保持在一起，請將 KeepWithGroup 設定為 **After**。  
  
-   `RepeatOnNewPage`. 布林值。 僅用於靜態資料列成員以及其中的 KeepWithGroup 不是 None 時。 如果有可能，在每個頁面上重複由 KeepWithGroup 所指定之至少一個動態成員執行個體的這個靜態資料列。 若要將資料列標頭與其相關聯的群組保持在一起，請將 RepeatOnNewPage 設定為 **True**。  
  
-   `Hidden`. 布林值。 指出一開始應該隱藏資料列或資料行。  
  
-   **ToggleItem：** 字串。 在其中加入切換影像之文字方塊的名稱。 文字方塊必須位於相同的群組範圍或包含範圍。  
  
 如需詳細資訊，請參閱[控制報表頁面上的 Tablix 資料區顯示 &#40;報表產生器及 SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)、[與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md) 和[在多個頁面上顯示資料列和資料行標頭 &#40;報表產生器及 SSRS&#41;](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)。  
  
 並非每個靜態成員在設計介面上都有一個對應到資料格的標頭。 在 [群組] 窗格中，下列慣例指出靜態成員是否沒有標頭：  
  
-   **Static** ：表示包含標頭資料格的靜態成員。  
  
-   **(Static)** ：表示不包含標頭資料格的靜態成員，亦即隱藏的靜態。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和精靈的報表產生器說明](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
