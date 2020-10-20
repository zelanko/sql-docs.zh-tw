---
description: 使用 Cube 及 Subcube 運算式
title: 使用 Cube 和子 Cube 運算式 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 37f23c75d8a947e52daf47ef9648ccbd1587b9a8
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192298"
---
# <a name="using-cube-and-subcube-expressions"></a>使用 Cube 及 Subcube 運算式


  您會以多維度運算式 (MDX) 陳述式使用 Cube 及 Subcube 運算式，以定義、操作或擷取 Cube 或 Subcube 的資料。  
  
## <a name="cube-expressions"></a>Cube 運算式  
 Cube 運算式不是包含 Cube 識別碼就是包含 CURRENTCUBE 關鍵字，因此只能是簡單運算式。 許多 MDX 陳述式會使用 CURRENTCUBE 關鍵字，以識別目前的 Cube 內容，而不是要求 Cube 識別碼。  
  
 Cube 識別碼在 MDX 語句的 BNF 標記法描述中會顯示為 *Cube_Name* 。  
  
 Cube 運算式可能會出現在幾個地方。 在 MDX SELECT 陳述式中，它們會指定擷取資料的目標 cube。 在下列範例查詢中，運算式 [Adventure Works] 會參考該名稱的 cube：  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 在 CREATE MEMBER 陳述式中，Cube 運算式會指定您所建立的導出成員會出現在哪一個 Cube 上。 在下列範例中，此陳述式會在 Adventure Works Cube 的 Measures 維度上建立導出量值：  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 當您在 MDX 指令碼內使用 CREATE MEMBER 陳述式時，可以使用 CURRENTCUBE 關鍵字取代 Cube 的名稱，因為要建立導出成員的 Cube 必須是 MDX 指令碼所屬的相同 Cube，如以下範例所示：  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 這樣做會使得從一個 Cube 將導出成員定義複製及貼到另一個 Cube 的作業變得更簡單，因為 Cube 的名稱不再是硬式編碼。  
  
## <a name="subcube-expressions"></a>SubCube 運算式  
 Subcube 運算式包含 Subcube 識別碼或是傳回 Subcube 的 MDX 陳述式。 如果 Subcube 運算式包含 Subcube 識別碼，它將會是簡單運算式。 如果它包含可傳回 Subcube 的 MDX 陳述式，它會是複雜陳述式。 例如，MDX SELECT 陳述式會傳回一個 Subcube，而且可以用於容許 Subcube 運算式之處，如下列範例所示：  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 在 FROM 子句中這樣使用 SELECT 陳述式也稱為子選擇。  
  
 遇到 Subcube 運算式的另一個常見案例就是在 MDX 指令碼中進行有設定範圍的指派。 在以下範例中，SCOPE 陳述式是用來將指派限制為由 [Measures].[Internet Sales Amount] 組成的 Subcube：  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 子工作的子工作識別碼會顯示為 *Subcube_Name*。 的形式出現在 MDX 陳述式的標記法描述內。  
  
## <a name="see-also"></a>另請參閱  
 [基本 MDX 查詢 &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query)   
 [在 MDX 中建立 Subcube &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)   
 [&#40;MDX&#41;建立子多維資料語句 ](../mdx/mdx-data-definition-create-subcube.md)   
 [MDX &#40;運算式&#41;](../mdx/expressions-mdx.md)   
 [SCOPE 陳述式 &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)  
  
