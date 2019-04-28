---
title: 將篩選新增至資料集 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eed37e74-6a43-4d7c-9959-2d5fa6a6aba9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bb2c717ca9d88d9c1ff1fe4f02fb89c46fe8f0e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62697760"
---
# <a name="add-a-filter-to-a-dataset-report-builder-and-ssrs"></a>將篩選加入至資料集 (報表產生器及 SSRS)
  從外部資料來源擷取資料後，將篩選加入至資料集來限制報表中的資料。 當您將篩選加入至資料集時，所有報表組件或資料區都只會使用符合篩選條件的資料。  
  
 若是共用資料集，套用至所有相依項目的篩選必須是報表伺服器上共用資料集定義的一部分。 包含共用資料集執行個體的報表或報表組件可以建立只套用至執行個體的其他篩選。  
  
 若要加入篩選，您必須指定一個或多個屬於篩選方程式的條件。 篩選方程式包含一個識別您想要篩選之資料的運算式、一個運算子和一個要比較的值。 篩選資料和值的資料類型必須相符。 不支援針對資料集的彙總值進行篩選。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-filter-to-a-shared-dataset"></a>若要將篩選加入至共用資料集  
  
1.  在共用資料集模式下，開啟共用資料集。  
  
2.  在 **[主資料夾]** 索引標籤的 **[共用資料集]** 群組中，按一下 [資料集]。 **[資料集屬性]** 對話方塊隨即開啟。  
  
3.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
4.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
5.  在 **[運算式]** 中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
6.  在清單方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
7.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
8.  在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]** 中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱[篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-filter-to-an-embedded-dataset-or-a-shared-dataset-instance"></a>若要將篩選加入至內嵌資料集或共用資料集執行個體  
  
1.  在報表設計模式下，開啟報表。  
  
2.  以滑鼠右鍵按一下 [報表資料] 窗格中的資料集，然後按一下 [資料集屬性]。 **[資料集屬性]** 對話方塊隨即開啟。  
  
3.  按一下 **[篩選]**。 這樣就會顯示目前的篩選方程式清單。 根據預設，此清單是空的。  
  
4.  按一下 **[加入]**。 新的空白篩選方程式隨即顯示。  
  
5.  在 **[運算式]** 中，針對要篩選的欄位輸入或選取運算式。 若要編輯運算式，請按一下運算式 (*fx*) 按鈕。  
  
6.  在下拉式方塊中，選取符合您在步驟 5 中建立之運算式資料類型的資料類型。  
  
7.  在 **[運算子]** 方塊中，選取您想要篩選用來比較 **[運算式]** 方塊和 **[值]** 方塊中值的運算子。 您所選擇的運算子會決定下一個步驟所使用的值數目。  
  
8.  在 **[值]** 方塊中，輸入您想要篩選在評估 **[運算式]** 中的值時，所針對的運算式或值。  
  
     如需篩選方程式的範例，請參閱[篩選方程式範例 &#40;報表產生器及 SSRS&#41;](../report-design/filter-equation-examples-report-builder-and-ssrs.md)。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [新增資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [加入篩選 &#40;報表產生器及 SSRS&#41;](../report-design/add-a-filter-report-builder-and-ssrs.md)  
  
  
