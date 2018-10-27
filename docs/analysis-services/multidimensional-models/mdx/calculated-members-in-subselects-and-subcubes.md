---
title: 子選擇和 Subcube 中導出成員 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8bae68e24f6a7f2dfd42e335a9e003f56cf1d610
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145313"
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>子選擇和 Subcube 中的導出成員
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  導出成員是值在執行階段從運算式計算而來的維度成員，它能用在子選擇和 Subcube 中以更精確地定義查詢的 Cubespace。  
  
## <a name="enabling-calculated-members-in-the-subspace"></a>啟用子空間中的導出成員  
 **的子查詢**中的連接字串屬性<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>或**DBPROPMSMDSUBQUERIES**中的屬性[支援的 XMLA 屬性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)定義的行為或允許導出的成員或導出的集合子選擇或 subcube 上。 在本文的內容中，除非另有說明，否則子選擇同時指子選擇和 Subcube。  
  
 SubQueries 屬性允許下列值。  
  
|||  
|-|-|  
|值|描述|  
|0|子選擇或 Subcube 中不允許使用導出成員。<br /><br /> 評估子選擇或 Subcube 時，如果參考導出成員就會引發錯誤。|  
|1|子選擇或 Subcube 中允許使用導出成員，但是在傳回的子空間中未導入上階成員。|  
|2|子選擇或 Subcube 中允許使用導出成員，而且在傳回的子空間中導入上階成員。 此外，在選取導出成員時允許使用混合資料粒度。|  
  
 如果在 SubQueries 屬性中使用值 1 或 2，即可允許導出成員用來篩選子選擇的傳回子空間。  
  
 範例將有助於釐清概念；首先必須建立導出成員，然後發出子選擇查詢，以示範上述行為。  
  
 下列範例會建立一個在 [Geography].[Geography] 階層的 Washington 州底下加入 [Seattle Metro] 市的導出成員。  
  
 若要執行範例，連接字串必須包含有 1 值的 SubQueries 屬性，而且所有 MDX 陳述式必須在相同工作階段中執行。  
  
> [!IMPORTANT]  
>  如果您使用 Management Studio 來測試查詢，請按一下連線管理員上的 [選項] 按鈕以存取其他連接字串屬性窗格，您可以在窗格內輸入 subqueries=1 或 2，允許子空間中的導出成員。  
  
 首先發出下列 MDX 運算式：  
  
```  
  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 接著發出下列 MDX 查詢，以查看子選擇中允許的導出成員。  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 取得的結果為：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2011|CY 2012|CY 2013|CY 2014|  
|Seattle Metro Agg|$2,383,545.69|1$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 如上述，當 SubQueries=1 時，傳回的子空間中沒有 [Seattle Metro] 的上階，因此 [Geography].[Geography].allmembers 只包含導出成員。  
  
 如果在連接字串中使用 SubQueries=2 來執行範例，取得的結果為：  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(Null)|(Null)|(Null)|(Null)|(Null)|  
|United States|(Null)|(Null)|(Null)|(Null)|(Null)|  
|Washington|(Null)|(Null)|(Null)|(Null)|(Null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 如上述，使用 SubQueries=2 時，傳回的子空間中有 [Seattle Metro] 的上階，但沒有這些成員的值，因為沒有可提供彙總的一般成員。 因此，在這個範例中，針對導出成員的所有上階成員提供 NULL 值。  
  
 若要了解以上的行為，請務必了解導出成員不同於一般成員，並不會提供其父系的彙總；前者表示只單獨依照導出成員來篩選，會導致空上階，因為沒有可提供產生子空間之彙總值的一般成員。 如果您將一般成員加入至篩選運算式，彙總值就會來自這些一般成員。 繼續上述的範例，如果 Oregon 州的 Portland 市以及 Washington 州的 Spokane 市加入至出現導出成員的相同軸中，如下列 MDX 運算式所示：  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 則會取得下列結果。  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|United States|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(Null)|(Null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(Null)|(Null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(Null)|(Null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 在以上的結果中，[All Geographies]、[United States]、[Oregon] 和 [Washington] 的彙總值來自 &[Portland]&[OR] 和 &[Spokane]&[WA] 的下階彙總。 沒有任何值來自導出成員。  
  
### <a name="remarks"></a>備註  
 子選擇或 Subcube 運算式中只允許使用全域或工作階段導出成員。 如果 MDX 運算式中擁有查詢導出成員，在評估子選擇或 Subcube 運算式時就會引發錯誤。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [查詢中的子選擇](../../../analysis-services/multidimensional-models/mdx/subselects-in-queries.md)   
 [支援的 XMLA 屬性 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)  
  
  
