---
title: CREATE SUBCUBE 陳述式 (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2b505de916ba274ebb69137aa3f61fe384386829
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742537"
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 資料定義-建立 SUBCUBE


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
  
 請參閱[SELECT 陳述式&#40;MDX&#41; ](../mdx/mdx-data-manipulation-select.md)如需有關 Select 陳述式的詳細的語法說明和**NON VISUAL**子句。  
  
## <a name="remarks"></a>備註  
 Subcube 定義內排除預設成員時，座標將會相應地變更。 對於可彙總的屬性而言，預設成員會移動到 [All] 成員。 對於不可彙總的屬性而言，預設成員會移動到存在於 Subcube 內的成員。 下表包含 Subcube 範例以及預設成員組合。  
  
|原始的預設成員|可以彙總|子選擇|修訂過的預設成員|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|是|{Time.Year.2003}|沒有變更|  
|Time.Year。[1997]|是|{Time.Year.2003}|Time.Year.All|  
|Time.Year。[1997]|否|{Time.Year.2003}|Time.Year。[2003]|  
|Time.Year。[1997]|是|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time.Year。[1997]|否|{Time.Year.2003, Time.Year.2004}|Either Time.Year.[2003] 或<br /><br /> Time.Year.[2004]|  
  
 [All] 會員將永遠存在於 Subcube 內。  
  
 Subcube 內容中建立的工作階段物件會在卸除 Subcube 時一併卸除。  
  
 如需有關 subcube 的詳細資訊，請參閱[在 MDX 中建立 Subcube &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)。  
  
## <a name="example"></a>範例  
 下列範例會建立 Subcube，將明顯 Cube 空間限制於國家 (地區) 為加拿大的成員。 然後它會使用**成員**函數來傳回 Geography 使用者定義階層-只傳回加拿大的層級的國家/地區的所有成員。  
  
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
|All Resellers|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
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
 [重要概念，在 MDX 中的&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 指令碼陳述式&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP SUBCUBE 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 陳述式&#40;MDX&#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
