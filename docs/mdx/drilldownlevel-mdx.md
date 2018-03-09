---
title: "DrilldownLevel (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLDOWNLEVEL
dev_langs: kbMDX
helpviewer_keywords: DrilldownLevel function
ms.assetid: 47531ce5-1ac0-4aa9-a85c-824fb5d21e7c
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: da071ef3ba43af94caf81e1016cb84a2bffc082f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="drilldownlevel-mdx"></a>DrilldownLevel (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  向下鑽研某個集合中的成員，至該集合所表示之最底層再往下一層的層級。  
  
 指定的層級的向下切入下是選擇性的但如果您要設定層級，您可以使用**層級運算式**或**索引層級**。 這些屬性彼此互斥。 最後，查詢中如有出現導出成員，可以指定引數將這些成員加入資料列集。  
  
## <a name="syntax"></a>語法  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>引數  
 *Set_Expression*  
 傳回集合的有效多維度運算式 (MDX) 運算式。  
  
 *Level_Expression*  
 (選擇性)。 MDX 運算式，明確地識別要向下鑽研的層級。 若指定了層級運算式，請略過下列索引引數。  
  
 *Index*  
 (選擇性)。 指定集合內向下鑽研階層編號的有效數值運算式。 您可以使用索引層級而不是 Level_Expression，以明確識別要向下鑽研的層級。  
  
 *Include_Calc_Members*  
 (選擇性)。 旗標，指出在向下鑽研層級中若有導出成員存在，是否要包含它們。  
  
## <a name="remarks"></a>備註  
 **DrilldownLevel**函式會傳回一組子成員以階層順序，根據指定集合中包含的成員。 會保留指定之集合中原始成員的順序，但在函數之結果集中的所有子成員則在其父成員底下。  
  
 假設有某個多層級階層式資料結構，您可以明確地選擇要向下鑽研的層級。 指定層級的方式有兩種，且互不相容。 第一種方法是將**level_expression**使用傳回的層級的替代方式的 MDX 運算式的引數是指定**索引**引數，使用指定的層級數目的數值運算式。  
  
 如果指定了層級運算式，函數只會擷取在指定之層級的成員其子系，以階層順序來建構集合。 若指定了層級運算式，該層級卻沒有成員，則會忽略該層級運算式。  
  
 如果指定索引值，假設以零為基底的索引，則此函數會只擷取指定之集合中所參考階層之最低層級再下一個層級的那些成員之子系，以階層順序來建構集合。  
  
 如果沒有指定層級運算式或索引值，此函數只會擷取指定之集合中所參考之第一個維度其最低層級的那些成員其子系，以階層順序來建構集合。  
  
 查詢 XMLA 屬性 MdpropMdxDrillFunctions，可讓您確認伺服器為鑽研函數; 提供的支援層級請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)如需詳細資訊。  
  
## <a name="examples"></a>範例  
 您可以在 SSMS 的 MDX 查詢視窗中使用 Adventure Works Cube，嘗試下列範例。  
  
 **範例 1 – 示範最基本的語法**  
  
 第一個範例顯示的最少語法**DrilldownLevel**。 唯一需要的引數是集合運算式。 請注意，當您執行此查詢，您取得父 [All Categories] 及下一個層級的成員向下: [Accessories]、 [Bikes] 等等。 雖然這個範例是簡單的它會示範的基本目的**DrilldownLevel**函式，會向下鑽研至下一層級。  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 範例 2 – 使用明確索引層級的替代語法  
  
 此範例示範替代語法，其中透過數值運算式指定了索引層級。 在此情況中，索引層級為 0。 就以零為基底的索引而言，則此為最低的層級。  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 請注意，結果集與上一個查詢相同。 一般而言，除非您想要使向下鑽研在特定的層級開始，否則就不必設定索引層級。 重新執行上一個查詢，並將索引值設為 1，然後再設為 2。 當索引值設為 1 時，您會看見向下鑽研從該階層的第二個層級開始。 當索引值設為 2 時，向下鑽研會在第三個層級開始，也就是此範例的最高層級。 數值運算式越高，索引層級也會越高。  
  
 **範例 3 – 示範層級的運算式**  
  
 下一個範例示範如何使用層級運算式。 假設某個集合代表某個階層結構，則使用層級運算式可讓您選擇階層中要開始向下鑽研的層級。  
  
 在此範例中，向下鑽研的層級會從 [City]，做為第二個引數**DrilldownLevel**函式。 當您執行此查詢時，會針對華盛頓州和奧勒岡州從 [City] 層級開始向下鑽研。 每個**DrilldownLevel**函式，結果集也包含在下一步 層級 [Postal codes] 下的成員。  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **範例 4 – 包含導出成員**  
  
 最後一個範例會示範導出的成員，會出現在結果底部設定當您將加入**include_calculated_members**旗標。 請注意，此旗標會指定為第四個參數。  
  
 因為導出成員和非導出成員位於相同的層級中，所以此範例為有效。 導出成員 [West Coast] 是由 [United States] 的成員，加上 [United States] 下一層的所有成員所組成。  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 若您只移除旗標，然後重新執行查詢，則會獲得相同的結果，但結果中不包含導出成員 [West Coast]。  
  
## <a name="see-also"></a>請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
