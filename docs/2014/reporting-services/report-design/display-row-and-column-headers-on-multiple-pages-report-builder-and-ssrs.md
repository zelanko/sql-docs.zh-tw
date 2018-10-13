---
title: 在多個頁面上顯示資料列和資料行標頭 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2422b1e2-822f-4379-9d7f-9afebb350e3f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 60bfb038d6712f44d6a0b5cd6cc57863f0f76ade
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2018
ms.locfileid: "48904978"
---
# <a name="display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs"></a>在多個頁面上顯示資料列和資料行標頭 (報表產生器及 SSRS)
  您可以控制是否要針對跨多個頁面的 Tablix 資料區，在每個頁面上重複資料列和資料行標頭。 Tablix 資料區可以是資料表、矩陣或清單。  
  
 控制資料列和資料行的方式，是根據 Tablix 資料區是否具有群組標題而定。 當您在具有群組標題的 Tablix 資料區內按一下時，虛線會顯示 Tablix 區域，如下圖中所示：  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 當您新增群組，使用 新增資料表或矩陣精靈 或 新增圖表精靈、 將欄位加入至 群組 窗格中，或使用操作功能表時，會自動建立資料列和資料行群組標頭。 如果 Tablix 資料區只有 Tablix 主體而沒有群組頁首，則資料行和資料列就是 Tablix 成員。  
  
 對靜態成員而言，您可以在多個頁面上顯示頂端相鄰的資料列或側邊相鄰的資料行。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-row-headers-on-multiple-pages"></a>若要在多個頁面上顯示資料列標頭  
  
1.  以滑鼠右鍵按一下 Tablix 資料區的資料列、資料行或角控點，然後按一下 **[Tablix 屬性]**。  
  
2.  在 **[資料列標頭]** 中，選取 **[在每一頁重複標頭資料列]**。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-column-headers-on-multiple-pages"></a>在多個頁面上顯示資料行標頭  
  
1.  以滑鼠右鍵按一下 Tablix 資料區的資料列、資料行或角控點，然後按一下 **[Tablix 屬性]**。  
  
2.  在 **[資料行標頭]** 中，選取 **[在每一頁重複標頭資料行]**。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-display-a-static-tablix-member-row-or-column-on-multiple-pages"></a>若要在多個頁面上顯示靜態 Tablix 成員 (資料列或資料行)  
  
1.  在設計介面上，按一下 Tablix 資料區的資料列或資料行控點來選取它。 [群組] 窗格會顯示資料列和資料行群組。  
  
2.  在 [群組] 窗格的右邊按一下向下箭頭，然後按一下 **[進階模式]**。 [資料列群組] 窗格會顯示資料列群組階層的階層式靜態及動態成員，[資料行群組] 窗格則會為資料行群組階層顯示類似的內容。  
  
3.  按一下對應至要在捲動時保持可見之靜態成員 (資料列或資料行) 的靜態成員。 [屬性] 窗格會顯示 **[Tablix 成員]** 屬性。  
  
     如果看不到 [屬性] 窗格，請按一下報表產生器視窗最上方的 **[檢視]** 索引標籤，然後按一下 **[屬性]**。  
  
4.  在 [屬性] 窗格中，將 **[RepeatOnNewPage]** 設定為 [True]。  
  
5.  將 **[KeepWithGroup]** 設定為 [After]。  
  
6.  針對您要重複的相鄰成員重複這個步驟。  
  
7.  預覽報表。  
  
 當您檢視 Tablix 資料區所跨越之報表的每個頁面時，靜態 Tablix 成員就會在每個頁面上重複。  
  
## <a name="see-also"></a>另請參閱  
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)   
 [控制分頁符號、標題、資料行和資料列 &#40;報表產生器及 SSRS&#41;](controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [與群組一起顯示頁首和頁尾 &#40;報表產生器及 SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)   
 [在報表中捲動時將標頭保持可見 &#40;報表產生器及 SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
  
