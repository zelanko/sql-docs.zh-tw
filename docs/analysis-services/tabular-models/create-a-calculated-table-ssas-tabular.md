---
title: 在 Analysis Services 表格式模型中建立導出的資料表 |Microsoft Docs
ms.date: 12/19/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 199096efcdf9212e19e1055f1276079eddfb1a75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62469366"
---
# <a name="create-a-calculated-table"></a>建立導出的資料表 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  *導出資料表* 是以 DAX 查詢或運算式為基礎的計算物件，衍生自相同模型中其他資料表的全部或部分。  
  
 導出資料表可以解決的一個常見的設計問題就是呈現特定內容中的角色扮演維度，以便您將它公開為用戶端應用程式中的查詢結構。  您可能還記得，角色扮演維度只是一個顯示在多個內容中的資料表 — 典型的例子就是 [Date] 資料表，根據外部索引鍵關聯性可顯示為 OrderDate、ShipDate 或 DueDate。 藉由明確地建立 ShipDate 的導出資料表，您可以取得一個和其他資料表一樣可以完全運作，用來進行查詢的獨立資料表。 另一個使用包含設定已篩選的資料列集的子集或超集資料行，從現有的資料表。 這可讓您保留原始的資料表，同時建立該資料表的變化以支援特定案例。  
  
 若要使用導出資料表的最佳優勢 ，您將至少需要了解部分 DAX。 當資料表使用運算式，它可能有助於了解導出的資料表包含具有 DAXSource，其中的運算式是 DAX 運算式的單一資料分割。  
運算式傳回的每個資料行都有一個 CalculatedTableColumn，其中傳回的資料行名稱為 SourceColumn (類似於非導出資料表上的 DataColumns)。 

您可以建立導出的資料表之前，至少一個資料表必須已經存在。 如果您要建立導出的資料表做為獨立計算的資料表物件，您可以先匯入資料來源的檔案 （csv、 xls、 xml） 來建立資料表。 您從匯入的檔案可以有單一資料行和單一值。 然後，您可以隱藏該資料表。 
  
## <a name="how-to-create-a-calculated-table"></a>如何建立導出資料表  
  
1.  首先，確認表格式模型具有 1200年或更高的相容性層級。 您可以檢查 SSDT 中模型上的 **相容性層級** 屬性。  
  
2.  切換至 [資料檢視]。 您無法在 [資料檢視] 中建立導出資料表。  
  
3.  選取 [資料表]   > [新的導出資料表]  。  
  
4.  輸入或貼上 DAX 運算式 (請參閱下方的一些概念)。  
  
5.  命名資料表。  
  
6.  建立與模型中的其他資料表的關聯性。 請參閱[建立關聯性資料表之間的兩個](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)如果您需要協助進行這個步驟。  
  
7.  參考模型中計算或運算式中的資料表，或使用 [在 Excel 中進行分析]  進行隨選資料瀏覽。  
  
### <a name="replicate-a-role-playing-dimension"></a>複寫角色扮演維度  
 在公式列中，輸入取得另一個資料表副本的 DAX 公式。 導出資料表填入之後，請為它提供描述性的名稱，然後設定使用特定角色之外部索引鍵的關聯性。 例如，在 Adventure Works 資料庫中，您可能會建立 [Due Date] 的導出資料表並使用 DueDateKey 作為事實資料表之關聯性的基礎。  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>彙總或已篩選的資料集  
 在 Formula 列中，輸入篩選、彙總，或操作資料集來包含您想要之資料列的 DAX 運算式。 此範例會依銷售量、顏色與貨幣分組。  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>使用多個資料表資料行的超集  
 在 Formula 列中，輸入結合多個資料表資料行的 DAX 運算式。 在此情況下，查詢輸出會列出每個貨幣的產品類別目錄。  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>另請參閱  
 [相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 中的資料分析運算式 &#40;DAX&#41;](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [了解表格式模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  
