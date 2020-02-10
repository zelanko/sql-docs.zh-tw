---
title: 新增運算式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 54505266a77c8baee7f39633ebccd0a5ab5708a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106734"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>加入運算式 (報表產生器及 SSRS)
  運算式會在整個報表中用來定義報表項目屬性、篩選、群組、排序次序、連接字串和參數值。 運算式是以等號（=）開頭，而且是以[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]撰寫。 運算式是由報表處理器在執行階段加以評估，這樣會將評估結果與報表配置元素結合。  
  
 運算式可能很簡單或很複雜。 簡單運算式會參考內建集合中的單一項目。 複雜運算式可包含常數、運算子、全域收集項和函數呼叫。 如需詳細資訊，請參閱[運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>將運算式加入文字方塊  
  
-   在 **[設計]** 檢視中，按一下設計介面上要在其中加入運算式的文字方塊。  
  
    -   如果是簡單運算式，請將運算式的顯示文字輸入文字方塊內。 例如，在資料集欄位 Sales 中輸入 `[Sales]`。  
  
    -   如果是複雜運算式，請以滑鼠右鍵按一下文字方塊，然後選取 **[運算式]**。 
  **[運算式]** 對話方塊隨即開啟。 在運算式窗格內的 '=' 後面輸入您的運算式或是以互動方式建立運算式，然後按一下 [確定]。  
  
         此運算式會以 `<<Expr>>`形式出現在設計介面上。  
  
## <a name="see-also"></a>另請參閱  
 [格式化文字和預留位置 &#40;報表產生器及 SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [文字方塊 &#40;報表產生器及 SSRS&#41;](text-boxes-report-builder-and-ssrs.md)   
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [篩選方程式範例 &#40;報表產生器和 SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [群組運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [運算式對話方塊 &#40;報表產生器&#41;](../expression-dialog-box-report-builder.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [將程式碼新增至 &#40;SSRS&#41;的報表](add-code-to-a-report-ssrs.md)  
  
  
