---
title: "準備要在 Tablix 資料區中顯示的資料 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
caps.latest.revision: "5"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 097b9e93906ecb166ae2b13aa5c3f6892241c4c2
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>準備要在 Tablix 資料區中顯示的資料 (報表產生器及 SSRS)
  Tablix 資料區域會顯示資料集中的資料。 您可以檢視針對資料集擷取的所有資料，或者您可以建立篩選，讓您僅能看到資料的子集。 您也可以加入條件式運算式來填入 Null 值，或修改資料集的查詢來包含定義現有資料行之排序次序的資料行。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>在欄位值中使用 Null 和空白  
 資料集中欄位集合的資料包含在執行階段從資料來源擷取的所有值，包括 Null 值和空白。 Null 值和空白通常無法分辨。 在大部分的情況下，這是所要的行為。 例如， [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) 和 [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md) 之類的數值彙總函式會忽略 Null 值。 如需詳細資訊，請參閱 [彙總函式參考 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)。  
  
 如果您不想要以不同的方式處理 Null 值，可以使用條件式運算式或自訂程式碼，將自訂值取代為 Null 值。 例如，下列運算式會在 `Null` 欄位中出現 Null 值的每個位置，取代文字 `[Size]`。  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 如需有關使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料來源擷取資料之前，排除資料中 Null 值的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server 線上叢書 [》中](http://go.microsoft.com/fwlink/?linkid=120955)文件集的＜Null 值＞和＜Null 值與聯結＞。  
  
## <a name="handling-null-field-names"></a>處理 Null 欄位名稱  
 只要欄位本身存在於查詢結果集中，就可以在運算式中測試 Null 值。 您可以從自訂程式碼中，測試欄位本身是否出現在執行階段從資料來源傳回的集合欄位中。 如需詳細資訊，請參閱[資料集 Fields 集合參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)。  
  
## <a name="adding-a-sort-order-column"></a>加入排序次序資料行  
 根據預設，您可以依字母順序排序資料集欄位中的值。 若要以不同的次序進行排序，您可以將新的資料行加入到資料集，定義您要在資料區域中使用的排序次序。 例如，若要先針對 `[Color]` 欄位進行排序並排序白色與黑色的項目，您可以加入 `[ColorSortOrder]`資料行，如以下查詢所示：  
  
```  
SELECT ProductID, p.Name, Color,  
   CASE  
      WHEN p.Color = 'White' THEN 1  
      WHEN p.Color = 'Black' THEN 2  
      WHEN p.Color = 'Blue' THEN 3  
      WHEN p.Color = 'Yellow' THEN 4  
      ELSE 5  
   END As ColorSortOrder  
FROM Production.Product p  
```  
  
 若要根據此排序次序排序資料表資料區域，將詳細資料群組的排序運算式設定為 `=Fields!ColorSortOrder.Value`。 如需詳細資訊，請參閱[在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
