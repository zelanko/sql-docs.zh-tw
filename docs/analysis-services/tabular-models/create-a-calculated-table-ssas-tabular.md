---
title: 建立導出的資料表 |Microsoft 文件
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3d7ff98a-82a9-4333-a7d3-7a95a6f2caf7
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4d2b864184f74c2d3e094c579eef88634e007815
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-calculated-table"></a>建立導出的資料表 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  *導出資料表* 是以 DAX 查詢或運算式為基礎的計算物件，衍生自相同模型中其他資料表的全部或部分。  
  
 導出資料表可以解決的一個常見的設計問題就是呈現特定內容中的角色扮演維度，以便您將它公開為用戶端應用程式中的查詢結構。  您可能還記得，角色扮演維度只是一個顯示在多個內容中的資料表 — 典型的例子就是 [Date] 資料表，根據外部索引鍵關聯性可顯示為 OrderDate、ShipDate 或 DueDate。 藉由明確地建立 ShipDate 的導出資料表，您可以取得一個和其他資料表一樣可以完全運作，用來進行查詢的獨立資料表。  
  
 導出資料表的第二個使用包含從現有的資料表設定已篩選的資料列集，或是資料行的子集或超集。 這可讓您保留原始的資料表，同時建立該資料表的變化以支援特定案例。  
  
 若要使用導出資料表的最佳優勢 ，您將至少需要了解部分 DAX。 當您針對資料表使用運算式時，了解導出資料表包含具有 DAXSource (其中運算式為 DAX 運算式) 的單一資料分割可能有所幫助。  
運算式傳回的每個資料行都有一個 CalculatedTableColumn，其中傳回的資料行名稱為 SourceColumn (類似於非導出資料表上的 DataColumns)。  
  
## <a name="how-to-create-a-calculated-table"></a>如何建立導出資料表  
  
1.  首先，確認表格式模型具有 1200年或更高的相容性層級。 您可以檢查 SSDT 中模型上的 **相容性層級** 屬性。  
  
2.  切換至 [資料檢視]。 您無法在 [資料檢視] 中建立導出資料表。  
  
3.  選取 [資料表] > [新的導出資料表]。  
  
4.  輸入或貼上 DAX 運算式 (請參閱下方的一些概念)。  
  
5.  命名資料表。  
  
6.  建立與模型中的其他資料表的關聯性。 請參閱[建立資料表之間的關聯兩個](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)如果您需要這個步驟的說明。  
  
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
 [Data Analysis Expressions &#40;DAX&#41;在 Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [了解表格式模型中的 DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  
