---
title: 報表和群組變數集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10404"
- sql12.rtp.rptdesigner.categorygroupproperties.variables.f1
- "10083"
- sql12.rtp.rptdesigner.seriesgroupproperties.variables.f1
- sql12.rtp.rptdesigner.reportproperties.variables.f1
- sql12.rtp.rptdesigner.groupproperties.variables.f1
- "10292"
- "10412"
ms.assetid: 4be5b463-3ce2-483d-a3c6-dae752cb543e
caps.latest.revision: 9
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a4a03cad2b19cc853c48a1614daea34cb2fb43ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132599"
---
# <a name="report-and-group-variables-collections-references-report-builder-and-ssrs"></a>報表和群組變數集合參考 (報表產生器及 SSRS)
  當您要進行的複雜計算是在報表的運算式中使用一次以上時，建議您建立一個變數。 您可以建立報表變數或群組變數。 變數名稱在報表中必須是唯一的。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-variables"></a>報表變數  
 報表變數可用來保存與時間相依之計算的值，例如貨幣匯率或時間戳記，或多次參考之複雜計算的值。 根據預設，報表變數只要計算一次，就可以供整份報表的運算式使用。 報表變數預設是唯讀的。 您可以變更預設值，將報表變數啟用為讀寫。 報表變數中的值會在整個工作階段中保留，直到再次處理報表。  
  
 若要新增報表變數，請開啟 [報表屬性] 對話方塊、按一下 [變數]，然後提供名稱及值。 名稱是區分大小寫、以字母為開頭而且沒有任何空格的字串。 名稱可以包含字母、數字或底線 (_)。  
  
 若要參考運算式中的變數，請使用全域集合語法，例如 `=Variables!CustomTimeStamp.Value`。 此值會在設計介面的文字方塊中顯示為 `<<Expr>>`。  
  
 您可以透過以下方式來使用報表變數：  
  
-   **唯讀使用** ：設定一次某個值，以建立報表工作階段的常數，例如，用來建立時間戳記。  
  
     文字方塊中的運算式會在使用者逐頁檢視報表時視需要進行評估；因此，動態值 (例如，包含 `Now()` 函式的運算式，此函式會傳回當日時間) 可能會在您向後一頁之後，使用 [上一頁] 按鈕返回時傳回不同的值。 您可藉由將報表變數的值設定為運算式 `=Now()`，然後將該變數加入至您的運算式，來確保在整個報表處理時都會使用相同的值。  
  
-   **讀寫使用** ：設定一次某個值，然後在報表工作階段中序列化該值。 變數的讀寫選項會比在報表定義的程式碼區塊中使用靜態變數提供更好的替代方案。  
  
     當您清除**唯讀**變數會設為變數時，可寫入的屬性選項`true`。 若要更新運算式的值，請使用 SetValue 方法，例如， `=Variables!MyVariable.SetValue("123")`。  
  
    > [!NOTE]  
    >  您無法控制報表處理器初始化變數，或評估更新變數之運算式的時間。 系統未定義變數初始化的執行順序。  
  
 如需工作階段的詳細資訊，請參閱[預覽 Reports in Report Builder](../report-builder/previewing-reports-in-report-builder.md)。  
  
## <a name="group-variables"></a>群組變數  
 群組變數可用來計算一次群組範圍內的複雜運算式。 群組變數只有在群組及其子群組的範圍內有效。  
  
 例如，假設資料區域針對不同稅率類別目錄的貨品顯示存貨資料，而您想要為每個類別目錄套用不同的稅率。 您會根據類別目錄將資料分組，並在父群組上定義 *Tax* 變數。 然後針對每個稅率類別目錄定義 *ItemTax* 的群組變數，並將每個不同的類別目錄子群組指派給正確的群組變數。 例如：  
  
-   對於以 `[Category]`為基礎的父群組，定義具有 *值的* Tax `[Tax]`變數。 假設類別目錄值為 Food 和 Clothing。  
  
-   對於以 `[Subcategory]`為基礎的子群組，則將 *ItemsTax* 變數定義為 `=Variables!Tax.Value * Sum(Fields!Price.Value)`。 假設 Food 類別目錄的子類別目錄值為 Beverages 和 Bread。 假設 Clothing 的子類別目錄值為 Shirts 和 Hats。  
  
-   針對子群組中資料列的文字方塊，加入 `=Variables!ItemsTax.Value`運算式。  
  
     該文字方塊會使用 Food 稅率顯示 Beverages 和 Bread 的總稅額，而使用 Clothing 稅率顯示 Shirts 和 Hats 的總稅額。  
  
 若要加入群組變數，請開啟 **[Tablix 群組屬性]** 對話方塊，按一下 **[變數]**，然後提供名稱及值。 群組變數會針對每個唯一的群組值計算一次。  
  
 若要參考運算式中的變數，請使用全域集合語法，例如 `=Variables!GroupDescription.Value`。 此值會在設計介面的文字方塊中顯示為 `<<Expr>>`。  
  
## <a name="see-also"></a>另請參閱  
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Built-in Collections in Expressions&#40;報表產生器和 SSRS&#41;](built-in-collections-in-expressions-report-builder.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  