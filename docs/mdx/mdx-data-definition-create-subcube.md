---
title: 建立子集語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f137e8c377c94a60fdcfd8f1534069cef4b28f66
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68887440"
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 資料定義 - CREATE SUBCUBE


  將指定 Cube 或 Subcube 的 Cube 空間重新定義為指定的 Subcube。 此陳述式會變更後續作業的明顯 Cube 空間。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供受限之 Cube 或檢視方塊名稱的有效字串運算式，此名稱會變成 Subcube 名稱。  
  
 *Select_Statement*  
 不包含 WITH、NON EMPTY 或 HAVING 子句，並且不要求維度或資料格屬性的有效多維度運算式 (MDX) SELECT 運算式。  
  
 如需 Select 語句和**非視覺化**子句的詳細語法說明，請參閱[SELECT 語句 &#40;MDX&#41;](../mdx/mdx-data-manipulation-select.md) 。  
  
## <a name="remarks"></a>備註  
 Subcube 定義內排除預設成員時，座標將會相應地變更。 對於可彙總的屬性而言，預設成員會移動到 [All] 成員。 對於不可彙總的屬性而言，預設成員會移動到存在於 Subcube 內的成員。 下表包含 Subcube 範例以及預設成員組合。  
  
|原始的預設成員|可以彙總|子選擇|修訂過的預設成員|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|是|{Time.Year.2003}|無變更|  
|時間. 年。[1997]|是|{Time.Year.2003}|Time.Year.All|  
|時間. 年。[1997]|否|{Time.Year.2003}|時間. 年。[2003]|  
|時間. 年。[1997]|是|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|時間. 年。[1997]|否|{Time.Year.2003, Time.Year.2004}|Either Time.Year.[2003] 或<br /><br /> Time.Year.[2004]|  
  
 [All] 會員將永遠存在於 Subcube 內。  
  
 Subcube 內容中建立的工作階段物件會在卸除 Subcube 時一併卸除。  
  
 如需 subcube 的詳細資訊，請參閱[在 mdx 中建立 subcube &#40;mdx&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)。  
  
## <a name="example"></a>範例  
 下列範例會建立 Subcube，將明顯 Cube 空間限制於國家 (地區) 為加拿大的成員。 然後，它會使用**MEMBERS**函式傳回 Geography 使用者定義階層之 country 層級的所有成員-只傳回加拿大的國家/地區。  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 下列範例會建立 Subcube，將明顯 Cube 空間限制於 Products.Category 中的 {Accessories, Clothing} 成員以及 Resellers.[Business Type] 中的 {[Value Added Reseller], [Warehouse]}。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 使用下列 MDX 查詢 Products.Category 和 Resellers.[Business Type] 中所有成員的 Subcube：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 產生結果如下：  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2031079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767388.52|$175,002.81|$592,385.71|  
|Warehouse|$1263690.86|$331,169.64|$932,521.23|  
  
 使用 NON VISUAL 子句卸除並重新建立 Subcube，會建立一個能夠保留 Products.Category 和 Resellers.[Business Type] 所有成員實際總計的 Subcube，不論這些成員在 Subcube 中是顯示或隱藏。  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 發出與上面相同的 MDX 查詢：  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 產生下列不同結果：  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 [All Products] 和 [All Resellers] 的資料行與資料列個別包含所有成員的總計，而不只是可見成員的總計。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 中的重要概念 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Mdx 腳本語句 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [&#40;MDX&#41;的 DROP 子資料集語句](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 語句 &#40;MDX&#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
