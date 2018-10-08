---
title: 格式化文字方塊中的文字 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: df0794b5-96b0-4034-bd17-1be7f31e29db
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b4d864f2d9f29e24fc8502a1e0f1c53c096cb61
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783976"
---
# <a name="format-text-in-a-text-box-report-builder-and-ssrs"></a>格式化文字方塊中的文字 (報表產生器及 SSRS)
  您可以在文件方塊中，單獨地對文字任何一部分進行格式化，並且在同一個文字方塊中，混合使用預留文字與靜態文字。 混合格式與加入預留位置文字的功能可以讓您針對報表中的文字建立合併列印或範本。 您可以使用預留位置來個別定義和格式化任何運算式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-combine-multiple-formats-in-a-text-box"></a>若要在文字方塊中結合多種格式  
  
1.  在 **[插入]** 索引標籤上，按一下 **[文字方塊]**。 按一下設計介面，然後拖曳滑鼠來建立一個所需大小的方塊。  
  
2.  在文字方塊內部，選取您想要格式化的文字。  
  
3.  以滑鼠右鍵按一下選取的文字，然後按一下 [文字屬性]。  
  
4.  設定格式選項。 例如，在 [一般] 索引標籤上：  
  
    -   **工具提示** ：輸入文字或評估為工具提示的運算式。 當使用者將滑鼠指標停留在報表的項目上方時，便會出現工具提示。  
  
    -   **標記類型** ：選取一個選項，指示要如何轉譯選取的文字：  
  
         **純文字** ：將選取的文字顯示為簡單的文字。 HTML 將視為常值文字。  
  
         **HTML**  將選取的文字顯示為 HTML。 如果預留位置的運算式值包含有效的 HTML 標記，這些標記將會轉譯為 HTML。 如需詳細資訊，請參閱[將 HTML 匯入至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)。  
  
5.  按一下 [確定] 。  
  
6.  針對您想要格式化的其餘文字，重複步驟 2 至 5。  
  
### <a name="to-format-text-and-placeholders-differently-in-the-same-text-box"></a>若要在相同的文字方塊中使用不同的方式格式化文字和預留位置  
  
1.  在 **[插入]** 索引標籤上，按一下 **[清單]**。 按一下設計介面，然後拖曳滑鼠來建立一個所需大小的方塊。 **[資料集屬性]** 對話方塊隨即開啟。 您可以使用共用資料集或在報表中內嵌資料集。 如需詳細資訊，請按一下[資料集屬性對話方塊、查詢 &#40;報表產生器&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) 或[資料集屬性對話方塊、查詢](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)。  
  
2.  在 **[插入]** 索引標籤上，按一下 **[文字方塊]**。 在清單中按一下，然後拖曳滑鼠來建立一個所需大小的方塊。  
  
3.  在文字方塊中輸入標籤，例如 **My Field**。  
  
4.  將欄位從資料集拖曳至文字方塊中。 如此就會針對您的欄位建立預留位置。  
  
5.  從基本格式中選取預留位置文字，然後在 [主資料夾] 索引標籤的 [字型] 群組中按一下其中一個格式選項。例如，按一下 [粗體] 按鈕。  
  
     如需其他格式選項，以滑鼠右鍵按一下預留位置文字，然後按一下 [預留位置屬性]。  
  
6.  按一下 [確定] 。 在 [報表設計] 檢視中，文字方塊中應該包含 "**My Field**: [*FieldName*]"，其中 *FieldName* 是您欄位的名稱。  
  
7.  按一下 **[執行]**。  
  
 清單會針對欄位中每一個值重複一次，而且 *FieldName* 預留位置每次都會由資料集中該欄位的值取代。  
  
## <a name="see-also"></a>另請參閱  
 [文字方塊 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [將 HTML 新增至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [預留位置屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
