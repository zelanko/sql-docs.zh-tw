---
title: 運算式對話方塊（報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
helpviewer_keywords:
- expressions
ms.assetid: e89c4d97-5d41-4b55-8695-79329edac15d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6f12a39c1456c179187654445947de9ee7d87a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109150"
---
# <a name="expression-dialog-box-report-builder"></a>運算式對話方塊 (報表產生器)
  使用 [**運算式**] 對話方塊可為[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]報表專案屬性撰寫運算式。 您可以使用運算式來設定許多屬性，包含色彩、字型和框線等。 在執行階段，報表處理器會評估運算式並取代屬性值的結果。  
  
 [運算式]**** 對話方塊包含程式碼視窗、類別目錄樹狀結構、類別目錄項目、描述窗格和範例窗格。 [**運算式**] 對話方塊會區分內容;類別目錄專案和描述會變更，以回應您所使用的運算式類別目錄。 如需詳細資訊，請參閱[運算式範例 &#40;報表產生器和 ssrs&#41;](report-design/expression-examples-report-builder-and-ssrs.md)、[運算式 &#40;報表產生器和 ssrs&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
## <a name="expression-constructs"></a>運算式建構  
 運算式是以等號 (=) 開始，可以包含常數、常值、運算子，以及內建欄位、內建集合、內建函數、 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 執行階段程式庫函數、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Common Language Runtime 類別和自訂函數的參考。 下列清單描述可加入運算式的類別目錄和值。  
  
 **為：**  _\<PropertyName>設定運算式_  
 為其定義運算式的屬性名稱。 您也可以在 [屬性] 窗格中依名稱設定這個屬性。  
  
 **常數**  
 針對以常數為基礎的屬性，提供對此屬性有效之預先定義值的清單。 例如，以色彩為基礎的屬性會顯示有效的色彩名稱。 對於是布林資料類型的屬性而言，值為 `True` 和 `False`。  
  
 並非所有支援運算式的項目都可設為常數。 如果屬性無法設為常數值，描述窗格會提供這項資訊。  
  
 **內建欄位**  
 提供全域集合裡您可以在運算式中使用之項目的清單。 有些集合只有在報表發行至伺服器後，才受到支援。 如需詳細資訊，請參閱[運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)。  
  
 **參數**  
 提供報表參數清單。  
  
 **欄位（** _ \<選取的資料集>_ **）**  
 顯示在 [資料集] 類別目錄中所選取之資料集的欄位清單。 按兩下欄位，即可將欄位複製至 [運算式]**** 方塊。  
  
 **Vsam**  
 提供可用資料集的清單，並顯示做為資料集之成員的欄位。  
  
 **變數**  
 顯示報表變數的清單。 如需詳細資訊，請參閱[報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)。  
  
 **運算子**  
 顯示您可以包含在計算或字串操作中的運算子。 如需詳細資訊，請參閱[運算式中的運算子 &#40;報表產生器及 SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md)。  
  
 **一般功能**  
 顯示一般函數，依類型分組。 當您在 [項目] 窗格中選取函數時，描述及範例就會顯示。  
  
 一般函數包含內建報表和彙總函式、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 執行階段程式庫函數，以及 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 和 <xref:System.Math> 命名空間中的 <xref:System.Convert> Common Language Runtime (CLR) 類別。 您也可以加入未出現在類別目錄清單中的 CLR 類別以及外部組件的參考。 如需詳細資訊，請參閱 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
## <a name="options"></a>選項。  
 程式碼視窗  
 使用上方窗格中的程式碼視窗，來輸入運算式。 當您開啟 [運算式]**** 對話方塊時，程式碼視窗會包含運算式。 您可以取代或修訂運算式。 您可以加入函數呼叫、運算子、常數、欄位、參數、全域集合的項目以及自訂程式碼的參考。 程式碼視窗會在您進行變更時顯示出變更。  
  
 波浪式紅色底線指出發生語法錯誤。 把滑鼠游標暫留在加底線文字上方，以查看錯誤訊息。  
  
 輸入後面接有標點符號分隔符號的全域集合詞彙時，您會看到可用成員或屬性的下拉式清單。 從下拉式清單中，您可輸入後面接有 Tab 的前幾個字元，以自動填入選項。  
  
 輸入函數名稱且在後面加上左括號時，您會看到工具提示提供有關參數和函數傳回值的資訊。  
  
 **類別目錄**  
 顯示運算式的類別目錄。 選擇類別目錄會為運算式的建立奠立內容，並會變更 [項目] 窗格中的有效值清單。 例如，針對文字方塊值的運算式，展開 [一般函數]，然後選取 [彙總函式]， `Avg`以`Count`顯示、和 [**專案**] 窗格中的其他函數。  
  
 **Item**  
 顯示所選取類別目錄的有效值清單。 請在項目上按兩下，以在程式碼視窗中的插入點加入這個項目的運算式文字。  
  
 **值**  
 第三個窗格會包含描述、範例運算式或有效值清單，依您選取的類別目錄和項目而定。 拖曳對話方塊的邊緣可加寬範例區域。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [篩選方程式範例 &#40;報表產生器和 SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [資料集欄位集合參考 &#40;報表產生器和 SSRS&#41;](report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)   
 [彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-design/report-builder-functions-aggregate-functions-reference.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [[選取色彩] 對話方塊 &#40;報表產生器和 SSRS&#41;](../../2014/reporting-services/select-color-dialog-box-report-builder-and-ssrs.md)  
  
  
