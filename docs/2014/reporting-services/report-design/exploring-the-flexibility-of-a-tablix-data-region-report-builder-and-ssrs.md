---
title: 探索 Tablix 資料區的彈性(報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fef19359-a618-4d21-a7e4-e391cdefd4eb
caps.latest.revision: 4
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d4dbdcedec7cf61b3de912bab3e3658c0267f134
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323888"
---
# <a name="exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs"></a>探索 Tablix 資料區的彈性(報表產生器及 SSRS)
  當您從功能區上的 [插入] 索引標籤加入資料表、矩陣或清單資料區域時，您會從 Tablix 資料區域的初始範本開始，但是您不會受到該範本的限制。 您可以加入或移除任何 Tablix 資料區域功能 (例如，群組、資料列和資料行)，藉以繼續開發資料顯示的方式。  
  
 當您刪除資料列或資料行群組時，可以選擇刪除用於顯示群組值的資料列和資料行。 您也可以手動加入或移除資料列和資料行。 若要了解如何用來顯示詳細資料和群組資料的資料列和資料行，請參閱[Tablix 資料區&#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)。  
  
 變更 Tablix 資料區域的結構之後，您可以設定屬性來協助控制報表呈現資料區域的方式，例如，您可以在每一頁的頂端重複資料行標頭，或保留包含此群組的群組頁首。 如需詳細資訊，請參閱[控制報表頁面上的 Tablix 資料區顯示 &#40;報表產生器及 SSRS&#41;](controlling-the-tablix-data-region-display-on-a-report-page.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="changing-a-table-to-a-matrix"></a>將資料表變更為矩陣  
 根據預設，資料表的詳細資料列會顯示來自報表資料集的值。 資料表通常會加入依群組組織詳細資料的資料列群組，然後根據每個群組加入彙總值。 若要將資料表變更為矩陣，請加入資料行群組。 通常您會在資料區域同時包含資料列和資料行群組時移除詳細資料群組，讓您可以只顯示群組的摘要值。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 根據定義，當您建立矩陣時，就會加入 Tablix 邊角資料格。 您可以在此區域合併資料格並加入標籤。 如需詳細資訊，請參閱[在資料區中合併資料格 &#40;報表產生器及 SSRS&#41;](merge-cells-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="changing-a-matrix-to-a-table"></a>將矩陣變更為資料表  
 根據預設，矩陣中包含資料列群組和資料行群組，但沒有詳細資料群組。 若要將矩陣變更為資料表，移除資料行群組，並加入要在詳細資料列上顯示的詳細資料群組。 如需詳細資訊，請參閱[在資料區中新增或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 和[新增詳細資料群組 &#40;報表產生器及 SSRS&#41;](add-a-details-group-report-builder-and-ssrs.md)。  
  
## <a name="changing-a-default-list-to-a-grouped-list"></a>將預設清單變更為群組清單  
 根據預設，清單中包含詳細資料列，但沒有群組。 若要變更清單來使用群組資料列，請重新命名詳細資料群組，並指定群組運算式。 如需詳細資訊，請參閱[在資料區中新增或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
## <a name="creating-stepped-displays"></a>建立階梯狀顯示  
 根據預設，當您將群組加入到 Tablix 資料區域時，資料列群組頁首區域中的資料格會在資料行中顯示群組值。 當您擁有巢狀群組時，每個群組都會在個別的資料行顯示。 若要建立階梯狀顯示，移除所有群組資料行而只留下一個群組資料行，然後將剩餘的資料行格式化，將群組階層顯示為縮排文字顯示。 如需詳細資訊，請參閱[建立階梯狀報表 &#40;報表產生器及 SSRS&#41;](create-a-stepped-report-report-builder-and-ssrs.md)。  
  
## <a name="adding-an-adjacent-details-group"></a>加入相鄰的詳細資料群組  
 根據預設，詳細資料群組是群組階層中，最內部的子群組。 您無法在詳細資料群組下建立巢狀群組。 您可以建立其他相鄰的詳細資料群組，例如，依照銷售額顯示前 5 個產品以及最後 5 個產品。 您可以針對每個群組加入篩選和排序運算式，因此，您可以在一個 Tablix 資料區域中顯示來自相同資料集中的兩個詳細資料檢視。 如需詳細資訊，請參閱[了解群組 &#40;報表產生器及 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)、[在資料區中新增或刪除群組 &#40;報表產生器及 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) 和[將篩選新增至資料集 &#40;報表產生器及 SSRS&#41;](../report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
