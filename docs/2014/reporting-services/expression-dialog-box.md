---
title: 運算式對話方塊 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
- sql12.rtp.rptdesigner.expression.f1
helpviewer_keywords:
- Expression dialog box [Reporting Services]
ms.assetid: e6c74ccb-4594-4d4f-b958-618d710e34eb
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 43f27ea78bec3f7b81f49d44a6bd56274367f2b5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021680"
---
# <a name="expression-dialog-box"></a>運算式對話方塊
  使用**運算式**對話方塊，即可撰寫[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vbprvb](../includes/vbprvb-md.md)]運算式的報表項目屬性。 您可以使用運算式來設定許多屬性，包含色彩、字型和框線等。 在執行階段，報表處理器會評估運算式並取代屬性值的結果。  
  
 運算式可能很簡單或很複雜。 您可以在設計介面上或對話方塊中的文字方塊中，直接輸入簡單的運算式。 若要建立複雜的運算式，請使用**運算式** 對話方塊。 您可以一次建立一個運算式。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)。  
  
 若要開啟 [運算式] 對話方塊，請按一下對話方塊中的 [運算式] (**fx**) 按鈕，或從 [屬性] 窗格的快速鍵功能表或下拉式清單選取 [運算式]。 如需詳細資訊，請參閱 <<c0> [ 運算式在報表中使用&#40;報表產生器及 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)。</c0>  
  
 [運算式] 對話方塊包含程式碼視窗、類別目錄樹狀結構、類別目錄項目、描述窗格和範例窗格。  
  
 [運算式] 對話方塊會區分內容。類別目錄項目和描述會根據您正在處理的運算式類別目錄而變更。 它支援 IntelliSense、陳述式完成、函數呼叫範例和語法著色，讓您能夠輕易偵測出語法錯誤。  
  
## <a name="expression-constructs"></a>運算式建構  
 運算式是以等號 (=) 開始，可以包含常數、常值、運算子，以及內建欄位、內建集合、內建函數、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 執行階段程式庫函數、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Common Language Runtime 類別和自訂函數的參考。 下列清單描述可加入運算式的類別目錄和值。  
  
 **設定運算式對象：**_\<PropertyName>_  
 為其定義運算式的屬性名稱。 您也可以在 [屬性] 窗格中依名稱設定這個屬性。  
  
 **常數**  
 針對以常數為基礎的屬性，提供對此屬性有效之預先定義值的清單。 例如，以色彩為基礎的屬性會顯示有效的色彩名稱。 對於是布林資料類型的屬性而言，值為 `True` 和 `False`。  
  
 並非所有支援運算式的項目都可設為常數。 如果屬性無法設為常數值，描述窗格會提供這項資訊。  
  
 **內建欄位**  
 提供全域集合裡您可以在運算式中使用之項目的清單。 有些集合只有在報表發行至伺服器後，才受到支援。 如需詳細資訊，請參閱[內建的全域和使用者參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)。  
  
 **參數**  
 提供報表參數清單。  
  
 **Fields(** _\<selected Dataset>_ **)**  
 顯示在 [資料集] 類別目錄中所選取之資料集的欄位清單。 按兩下欄位，即可將欄位複製至 [運算式] 方塊。  
  
 **資料集**  
 提供可用資料集的清單，並顯示做為資料集之成員的欄位。  
  
 **變數**  
 顯示報表變數的清單。 如需詳細資訊，請參閱[報表和群組變數集合參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)。  
  
 **運算子**  
 顯示您可以包含在計算或字串操作中的運算子。 如需詳細資訊，請參閱[運算式中的運算子 &#40;報表產生器及 SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md)。  
  
 **常見的函式**  
 顯示一般函數，依類型分組。 當您在 [項目] 窗格中選取函數時，描述及範例就會顯示。  
  
 一般函數包含內建報表和彙總函式、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 執行階段程式庫函數，以及 <xref:System.Math> 和 <xref:System.Convert> 命名空間中的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 類別。 您也可以加入未出現在類別目錄清單中的 CLR 類別以及外部組件的參考。 如需詳細資訊，請參閱[報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
## <a name="options"></a>選項。  
 程式碼視窗  
 使用上方窗格中的程式碼視窗，來輸入運算式。 當您開啟 [運算式] 對話方塊時，程式碼視窗會包含運算式。 您可以取代或修訂運算式。 您可以加入函數呼叫、運算子、常數、欄位、參數、全域集合的項目以及自訂程式碼的參考。 程式碼視窗會在您進行變更時顯示出變更。  
  
 波浪式紅色底線指出發生語法錯誤。 把滑鼠游標暫留在加底線文字上方，以查看錯誤訊息。  
  
 輸入後面接有標點符號分隔符號的全域集合詞彙時，您會看到可用成員或屬性的下拉式清單。 從下拉式清單中，您可輸入後面接有 Tab 的前幾個字元，以自動填入選項。  
  
 輸入函數名稱且在後面加上左括號時，您會看到工具提示提供有關參數和函數傳回值的資訊。  
  
 **分類**  
 顯示運算式的類別目錄。 選擇類別目錄會為運算式的建立奠立內容，並會變更 [項目] 窗格中的有效值清單。 比方說，針對文字方塊值的運算式，依序展開 一般函數，然後選取要顯示的彙總函式`Avg`， `Count`，和在其他函式**項目**窗格。  
  
 **項目**  
 顯示所選取類別目錄的有效值清單。 請在項目上按兩下，以在程式碼視窗中的插入點加入這個項目的運算式文字。  
  
 **值**  
 第三個窗格會包含描述、範例運算式或有效值清單，依您選取的類別目錄和項目而定。 拖曳對話方塊的邊緣可加寬範例區域。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [參數集合參考 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [篩選方程式範例 &#40;報表產生器及 SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [運算式中的內建集合 &#40;報表產生器及 SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md)   
 [加入運算式 &#40;報表產生器及 SSRS&#41;](report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
