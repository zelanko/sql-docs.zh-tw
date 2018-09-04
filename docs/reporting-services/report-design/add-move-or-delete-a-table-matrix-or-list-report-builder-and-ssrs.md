---
title: 新增、移動或刪除資料表、矩陣或清單 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e7b2ed1c1664f3841ed2671a7d32bb2dacb1d20
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280210"
---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>加入、移動或刪除資料表、矩陣或清單 (報表產生器及 SSRS)
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，資料區會顯示報表資料集中的資料。 資料區包括資料表、矩陣、清單、圖表和量測計。 若要讓某個資料區以巢狀結構的方式置於另一個資料區內，請個別加入每一個資料區，然後將子資料區拖曳到父資料區。  
  
 將資料表或矩陣資料區加入至報表最簡單的方式就是執行新增資料表或新增矩陣精靈。 這些精靈會引導您完成選擇資料來源的連接、排列欄位，以及選擇配置和樣式的程序。 您只能在報表產生器中使用這些精靈。  
  
## <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>若要使用新增資料表或新增矩陣精靈，將資料表或矩陣加入至報表  
  
1.  在 **[插入]** 索引標籤上，按一下 **[資料表]** 或 **[矩陣]**，然後按一下 **[資料表精靈]** 或 **[矩陣精靈]**。  
  
2.  遵循 [新增資料表] 或 [新增矩陣] 精靈中的步驟進行。  
  
3.  在 **[主資料夾]** 索引標籤上，按一下 **[執行]** 查看轉譯的報表。  
  
4.  在 **[執行]** 索引標籤上，按一下 **[設計]** 繼續處理報表。  
  
## <a name="to-add-a-data-region"></a>若要加入資料區  
  
1.  在 **[功能區]** 的 **[資料區域]** 群組中，按一下要加入的資料區。  
  
2.  按一下設計介面，然後拖曳滑鼠來建立一個方塊，這就是您想要的資料區大小。  
  
3.  將報表資料集欄位從 [報表資料] 窗格拖曳到資料區資料格上。 資料區現在會繫結至報表資料集中的資料。  
  
## <a name="to-select-a-data-region"></a>若要選取資料區  
  
-   若為 Tablix 資料區，請以滑鼠右鍵按一下角控點。 若為圖表或量測計資料區，請在資料區中按一下。  
  
     隨即出現選取控點和八個調整大小的控點。  
  
     若為巢狀資料區，請在巢狀資料區中按一下滑鼠右鍵、按一下 [選取]，然後選取您想要的報表項目。 若要確認哪一個報表項目已選取，請使用 [屬性] 窗格。 設計介面上選取的項目名稱會出現在 [屬性] 窗格的工具列中。  
  
## <a name="to-move-a-data-region"></a>若要移動資料區  
  
-   若要移動資料區，請按一下資料區的選取控點，然後拖曳它。 使用貼齊格線，將它與現有的報表項目對齊。  
  
     如果看不到尺規，請按一下 [檢視] 索引標籤，並選取 **[尺規]** 選項。  
  
     另外，您也可以使用方向鍵，將選取的資料區移到設計介面上。  
  
## <a name="to-delete-a-data-region"></a>若要刪除資料區  
  
-   選取資料區，在資料區中按一下滑鼠右鍵，然後按一下 [刪除]。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
