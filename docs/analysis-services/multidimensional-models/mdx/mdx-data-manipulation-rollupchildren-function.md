---
title: 使用 RollupChildren 函數 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 135ab6e43a0b751639bd1ce1d93bf2183039f713
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>MDX 資料操作 RollupChildren 函數
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  多維度運算式 (MDX) [RollupChildren](../../../mdx/rollupchildren-mdx.md) 函數可積存成員的子系，將不同的一元運算子套用至每個子系，然後將此積存的值以數字傳回。 一元運算子可由與子成員相關的成員屬性提供，或者可能是字串運算式直接將運算子提供給函數。  
  
## <a name="rollupchildren-function-examples"></a>RollupChildren 函數範例  
 使用多維度運算式 (MDX) 陳述式之 **RollupChildren** 函數的說明很簡單，但此函數對 MDX 查詢的影響相當廣泛。  
  
 **RollupChildren** 函數會對為了對現有的 Cube 資料，執行選擇性分析而設計 MDX 查詢的產生影響。 例如，下表包含 Net Sales 父成員的子成員清單，以及在括弧中顯示它們的一元運算子 (以 **UNARY_OPERATOR** 成員屬性代表)。  
  
|父成員|子成員|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 Net Sales 父成員目前是淨銷售量的總和減去國內外總銷售量值，而國內外退貨量則當做積存減去。  
  
 但是，您想要外加 10% 以簡單、快速地預測國內外銷售總額，而不理會國內外的退貨量。 若要計算此值，您能以下其中一個方式使用 **RollupChildren** 函數：利用自訂成員屬性，或利用 **IIf** 函數。  
  
### <a name="using-a-custom-member-property"></a>使用自訂成員屬性  
 如果將會經常執行積存計算作業，其中一個方法是建立一個成員屬性，儲存供每個子系當做特定函數使用的運算子。 下表顯示有效的一元運算子，而且描述了預期的結果。  
  
|運算子|結果|  
|--------------|------------|  
|+|總計 = 總計 + 目前的子系|  
|-|總計 = 總計 - 目前的子系|  
|*|總計 =總計 * 目前的子系|  
|/|總計 =總計 / 目前的子系|  
|~|子系不會被用在積存中。 子系的值會被忽略。|  
  
 例如，您可以建立一個稱為 **SALES_OPERATOR** 的成員屬性，將以下的一元運算子指派給此成員屬性，如下表所示。  
  
|父成員|子成員|  
|-------------------|------------------|  
|Net Sales|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 有了這個新的成員屬性，以下 MDX 陳述式就可以快速且有效地執行銷售總額估計作業 (忽略國內外退貨量)：  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 當呼叫此函數時，就會使用成員屬性中儲存的運算子，將每個子系的值套用到總計。 國內外退貨量會被忽略，而且 **RollupChildren** 函數所傳回的積存總計會乘以 1.1。  
  
### <a name="using-the-iif-function"></a>使用 IIf 函數  
 如果範例作業不會經常執行，或如果該作業只會套用到一個 MDX 查詢，那麼 [IIf](../../../mdx/iif-mdx.md) 函數跟 **RollupChildren** 函數搭配使用，就可以提供相同的結果。 以下的 MDX 查詢可以提供跟先前 MDX 範例一樣的結果，但不需要使用自訂的成員屬性就可以做到。  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 MDX 陳述式會檢查子成員的一元運算子。 如果一元運算子用於減法 (如同在處理國內外退貨量成員的情況下)，則 **IIf** 函數會取代波狀符號 (~) 一元運算子。 否則， **IIf** 函數會使用子成員的一元運算子。 最後，傳回的積存總計會乘以 1.1，做為國內外銷售總額的預測值。  
  
## <a name="see-also"></a>另請參閱  
 [操作資料 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
