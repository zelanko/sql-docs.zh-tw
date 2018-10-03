---
title: 了解行程順序和求解順序 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- evaluation order [MDX]
- calculation order [MDX]
- SOLVE_ORDER property
- queries [MDX], solve orders
- solve orders [MDX]
- pass orders [MDX]
- expressions [MDX], solve orders
ms.assetid: 7ed7d4ee-4644-4c5d-99a4-c4b429d0203c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d8d1797bc1ffdf937e37fb1ffae075691a892ab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083008"
---
# <a name="understanding-pass-order-and-solve-order-mdx"></a>了解行程順序與解決順序 (MDX)
  當 Cube 做為 MDX 指令碼的計算結果時，Cube 會根據所使用的各種計算相關功能來進行多個計算階段。 每個階段都稱為一個計算行程。  
  
 計算行程可以是序數位置，稱為計算行程數目。 完整計算 Cube 中所有資料格所需的計算行程數目稱為 Cube 的計算行程深度。  
  
 事實資料表和回寫資料只會影響行程 0。 行程 0 之後，指令碼會擴展資料；指令碼中每個指派和計算陳述式都會建立新的行程。 在 MDX 指令碼之外，對絕對行程 0 的參考會參考指令碼為 Cube 所建立的最後行程。  
  
 導出成員會在所有行程建立，但運算式只會在目前行程套用。 先前的行程包含導出量值，不過會是 Null 值。  
  
## <a name="solve-order"></a>解決順序  
 解決順序決定在運算式發生競爭事件時，計算的優先權。 在單一行程內，解決順序決定兩件事情：  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 評估維度、成員、導出成員、自訂積存和導出資料格的順序。  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 評估自訂成員、導出成員、自訂積存和導出資料格的順序。  
  
 擁有最高解決順序的成員優先。  
  
> [!NOTE]  
>  此優先順序的例外狀況是彙總函式。 具有彙總函式的導出成員，其解決順序比任何交集的導出量值還低。  
  
## <a name="solve-order-values-and-precedence"></a>解決順序值和優先順序  
 解決順序值的範圍可以從 -8181 到 65535。 在此範圍中，某些解決順序值是對應到特定的計算種類，如下表所示。  
  
|計算|解決順序|  
|-----------------|-----------------|  
|自訂成員公式|-5119|  
|一元運算子|-5119|  
|視覺化總計計算|-4096|  
|其他所有計算 (若沒有特別指定)|0|  
  
 強烈建議您在設定解決順序值時只使用正整數。 如果您指定比上表中解決順序值還低的值，計算行程可能會變得無法預測。 例如，導出成員的計算會收到一個低於預設自訂積存公式值 -5119 的解決順序值。 這類低的解決順序值會造成導出成員的計算早於自訂積存公式，所以會產生不正確的結果。  
  
### <a name="creating-and-changing-solve-order"></a>建立與變更解決順序  
 在 [Cube 設計師] 的 [計算窗格] 上，您可以變更計算的順序，來變更導出成員和導出資料格的解決順序。  
  
 在 MDX 中，您可以使用 `SOLVE_ORDER` 關鍵字來建立或變更導出成員與導出資料格。  
  
## <a name="solve-order-examples"></a>解決順序範例  
 為了方便說明解決順序的可能複雜性，下列 MDX 查詢以兩個查詢開始，而個別查詢沒有解決順序的問題。 當這兩個查詢結合成一個查詢時，就需要解決順序。  
  
> [!NOTE]  
>  您可以針對 Adventure Works 範例多維度資料庫執行這些 MDX 查詢。 您可以從 codeplex 網站下載 [AdventureWorks Multidimensional Models SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) (AdventureWorks 多維度模型 SQL Server 2012) 範例。  
  
### <a name="query-1differences-in-income-and-expenses"></a>查詢 1—收益和費用的差異  
 在第一個 MDX 查詢中，建構一個簡單的 MDX 查詢來計算每年銷售和成本的差異，如以下範例所示：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 在此查詢中，只有一個導出成員 `Year Difference`。 因為只有一個導出成員，只要 Cube 不使用任何導出成員，就沒有解決順序的問題。  
  
 此 MDX 查詢產生類似下表的結果集。  
  
||Internet Sales Amount|Internet Total Product Cost|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**Year Difference**|($20,160.56)|$2,878.06|  
  
### <a name="query-2percentage-of-income-after-expenses"></a>查詢 2—扣除費用後的收益百分比  
 在第二個查詢中，使用以下 MDX 查詢來計算每年扣除費用後的收益百分比：  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 此 MDX 查詢和前一個查詢類似，只有一個導出成員 `Profit Margin`，因此也沒有任何求解順序的問題。  
  
 此 MDX 查詢產生類似下表，但有些微差異的結果集。  
  
||Internet Sales Amount|Internet Total Product Cost|獲利率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 第一個查詢和第二個查詢之間的結果集差異，在於導出成員的位置差異。 在第一個查詢中，導出成員是 ROWS 座標軸的一部份，而不是第二個查詢中的 COLUMNS 座標軸。 此種位置的差異在下一個查詢 (結合單一 MDX 查詢的兩個導出成員) 中就變得很重要。  
  
### <a name="query-3combined-year-difference-and-net-income-calculations"></a>查詢 3—結合年度差異和淨收益的計算  
 在結合上述兩個範例到單一 MDX 查詢的最終查詢中，求解順序就變得很重要，因為會同時計算資料行和資料列。 若要確定正確的順序，進行計算，定義所使用之計算發生的順序`SOLVE_ORDER`關鍵字。  
  
 `SOLVE_ORDER` 關鍵字指定 MDX 查詢中導出成員或 `CREATE MEMBER` 命令的解決順序。 搭配使用的整數值`SOLVE_ORDER`關鍵字是相對值，不需要從零開始，也不需要連續。 此數值只是告知 MDX 根據有較高值的成員計算所得出的值來導出成員。 如果導出的成員定義沒有`SOLVE_ORDER`關鍵字，預設值的導出成員為零。  
  
 例如，如果您結合前兩個範例查詢中使用的計算，兩個導出成員 `Year Difference` 和 `Profit Margin`會在 MDX 查詢範例之結果資料集中的單一資料格中產生交集。 決定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何評估此資料格的唯一方式，就是解決順序。 用來建立此資料格的公式會根據兩個導出成員的解決順序，來產生不同的結果。  
  
 首先，請嘗試結合以下 MDX 查詢中前兩個查詢所使用的計算：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 在此結合的 MDX 查詢範例中， `Profit Margin` 擁有最高的解決順序，所以當兩個運算式有交集時會優先處理它。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會使用 `Profit Margin` 公式來評估有問題的資料格。 此巢狀計算的結果，如下表所示。  
  
||Internet Sales Amount|Internet Total Product Cost|獲利率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|114.28%|  
  
 共用資料格中的結果是以 `Profit Margin`的公式為基礎。 也就是說， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會計算含有 `Year Difference` 資料之共用資料格的結果，產生下列公式 (為了清楚起見，結果為四捨五入)：  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 中的多個  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 這明顯錯誤。 但是，如果您在 MDX 查詢中切換導出成員的求解順序， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會以不同方式計算共用資料格的結果。 以下結合的 MDX 查詢改變了導出成員的解決順序：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 當切換導出成員的求解順序後， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會使用 `Year Difference` 公式來評估資料格，如下表所示。  
  
||Internet Sales Amount|Internet Total Product Cost|獲利率|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|(0.15%)|  
  
 因為此查詢使用含有 `Year Difference` 資料的 `Profit Margin` 公式，所以共用資料格的公式會類似以下計算：  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 或  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>其他考量  
 若 Cube 有大量的維度，並牽涉到導出成員、自訂積存公式或導出資料格時，處理解決順序會是非常複雜的問題。 當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 評估 MDX 查詢時， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 會考慮給定行程內牽涉到的所有項目 (包括 MDX 查詢中指定之 Cube 的維度) 的解決順序值。  
  
## <a name="see-also"></a>另請參閱  
 [CalculationCurrentPass &#40;MDX&#41;](/sql/mdx/calculationcurrentpass-mdx)   
 [CalculationPassValue &#40;MDX&#41;](/sql/mdx/calculationpassvalue-mdx)   
 [CREATE MEMBER 陳述式&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [操作資料&#40;MDX&#41;](mdx-data-manipulation-manipulating-data.md)  
  
  
