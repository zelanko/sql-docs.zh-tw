---
title: 基本 MDX 查詢 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7f3a1610f19bc99ce063d815f74906f10ddc2c7f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026605"
---
# <a name="mdx-query---the-basic-query"></a>MDX 查詢的基本查詢
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  基本的多維度運算式 (MDX) 查詢是 SELECT 陳述式，為 MDX 中最常使用的查詢。 了解 MDX SELECT 陳述式必須指定結果集的方式、SELECT 陳述式的語法為何，以及如何使用 SELECT 陳述式建立簡單查詢之後，您將完全了解如何使用 MDX 來查詢多維度資料。  
  
## <a name="specifying-a-result-set"></a>指定結果集  
 在 MDX 中，SELECT 陳述式會指定一個結果集，內含從 Cube 傳回的多維度資料子集。 若要指定結果集，MDX 查詢必須包含下列資訊：  
  
-   您要在結果集中包含的軸數目。 在一個 MDX 查詢中，您最多可指定 128 個座標軸。  
  
-   要在 MDX 查詢的每一個軸上包含的成員或 Tuple 集合。  
  
-   設定 MDX 查詢內容的 Cube 的名稱。  
  
-   要在 slicer 軸上包含的成員或 Tuple 集合。 如需 slicer 與查詢軸的詳細資訊，請參閱[利用查詢與 Slicer 軸限制查詢 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)。  
  
 為了識別查詢軸、要查詢的 Cube 以及 slicer 軸，MDX SELECT 陳述式會使用以下子句：  
  
-   SELECT 子句，決定 MDX SELECT 陳述式的查詢座標軸。 如需在 SELECT 子句內建構查詢軸的詳細資訊，請參閱[指定查詢軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
-   決定要查詢之 Cube 的 FROM 子句。 如需 FROM 子句的詳細資訊，請參閱 [SELECT Statement &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)。  
  
-   選擇性的 WHERE 子句，這個子句會決定要在 slicer 軸上用來限制所傳回資料的成員或 Tuple。 如需在 WHERE 子句內建構 slicer 軸的詳細資訊，請參閱[指定 Slicer 軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
> [!NOTE]  
>  如需 SELECT 陳述式不同子句的詳細資訊，請參閱 [SELECT 陳述式 &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)。  
  
## <a name="select-statement-syntax"></a>SELECT 陳述式語法  
 以下語法顯示基本 SELECT 陳述式，包括 SELECT、FROM 與 WHERE 子句的用法：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 MDX SELECT 陳述式支援選擇性語法，例如 WITH 關鍵字、使用 MDX 函數建立計算的成員以納入軸或 slicer 軸，以及做為查詢的一部分傳回特定資料格屬性值的能力。 如需 MDX SELECT 陳述式的詳細資訊，請參閱 [SELECT Statement &#40;MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)。  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>比較 MDX SELECT 陳述式與 SQL 的語法  
 MDX SELECT 陳述式的語法格式跟 SQL 的語法格式相似。 但是，有幾個基本的相異之處：  
  
-   MDX 語法使用括住 Tuple 或成員的大括號 ({ 與 } 字元) 來區分集合。如需成員、Tuple 以及集合語法的詳細資訊，請參閱[使用成員、Tuple 和集合 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)。  
  
-   在 SELECT 陳述式中，MDX 查詢可以有 0、1、2 或最多 128 個查詢軸。 每一個軸都會以完全相同的方式執行，不像 SQL 中查詢的資料列和資料行的行為模式大相逕庭。  
  
-   如同 SQL 查詢，FROM 子句為 MDX 查詢的資料來源命名。 但是，MDX FROM 子句僅限於單一 Cube。 使用 LookupCube 函數，就能按值逐一擷取其他 Cube 的資訊。  
  
-   WHERE 子句會描述 MDX 查詢中的 slicer 軸。 它的行為像是隱藏在查詢中的額外軸，會切割結果集的資料格中出現的值；不過它不像 SQL 的 WHERE 子句，不會直接影響查詢之資料列軸的結果。 SQL WHERE 子句的功能可透過其他 MDX 函數 (例如 FILTER 函數) 提供。  
  
## <a name="select-statement-example"></a>SELECT 陳述式範例  
 以下範例顯示使用 SELECT 陳述式的基本 MDX 查詢。 此查詢會傳回一個結果集，其中包含 Southwest 銷售區域在 2002 與 2003 年的銷售與稅額。  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 在此範例中，查詢定義了下列結果集資訊：  
  
-   SELECT 子句將查詢座標軸設為 Measures 維度的 Sales Amount 與 Tax Amount 成員，以及 Date 維度的 2002 與 2003 成員。  
  
-   FROM 子句指出資料來源是 Adventure Works Cube。  
  
-   WHERE 子句將 slicer 座標軸定義為 Sales Territory 維度的 Southwest 成員。  
  
 請注意，查詢範例也會使用 COLUMNS 與 ROWS 座標軸別名。 而這些座標軸的序數位置已經被使用。 以下範例顯示要如何撰寫 MDX 查詢，以使用每個座標軸的序數位置：  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 如需詳細範例，請參閱[指定查詢軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md) 和[指定 Slicer 軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
## <a name="see-also"></a>另請參閱  
 [MDX & #40; 中的重要概念Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [SELECT 陳述式 & #40;MDX & #41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
