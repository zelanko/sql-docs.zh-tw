---
title: "CREATE SUBCUBE 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SUBCUBE
- CREATE SUBCUBE
- CREATE
- SUBCUBE
dev_langs: kbMDX
helpviewer_keywords:
- subcubes [MDX]
- CREATE SUBCUBE statement
ms.assetid: 15b6ac4c-b68a-4f9f-b33c-f5f7c4a74535
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5fd57d53dd07238781c452730f00e526fb6c2fff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 資料定義-建立 SUBCUBE
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 請參閱[選取陳述式 &#40;MDX &#41;](../mdx/mdx-data-manipulation-select.md)如需有關 Select 陳述式的詳細的語法說明和**NON VISUAL**子句。  
  
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
  
 如需有關 subcube 的詳細資訊，請參閱[在 MDX &#40; 中建立 SubcubeMDX &#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md).  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [MDX &#40; 中的重要概念Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 指令碼陳述式 &#40;MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP SUBCUBE 陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 陳述式 &#40;MDX &#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
