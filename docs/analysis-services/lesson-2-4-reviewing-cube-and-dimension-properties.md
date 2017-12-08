---
title: "檢閱 Cube 和維度屬性 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 73dea5a137a6ae685d36f06a4e4497e976133819
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-4---reviewing-cube-and-dimension-properties"></a>課程 2-4-檢閱 Cube 和維度屬性
定義 Cube 之後，您可以使用 Cube 設計師來檢閱這些結果。 在下列工作中，您將檢閱 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中 Cube 的結構。  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>若要在 Cube 設計師中檢閱 Cube 和維度屬性  
  
1.  若要開啟 Cube 設計師，請在方案總管的 [Cube] 節點中，按兩下 [Analysis Services 教學課程] Cube。  
  
2.  在 Cube 設計師中，於 [Cube 結構] 索引標籤的 [量值] 窗格中，展開 [網際網路銷售] 量值群組來顯示定義的量值。  
  
    您可以將量值拖曳到您要的順序，藉以變更順序。 您所建立的順序會影響某些用戶端應用程式排列這些量值的方式。 量值群組和它包含的每一個量值都有屬性，您可以在 [屬性] 視窗中編輯它們。  
  
3.  在 Cube 設計師中，於 [Cube 結構] 索引標籤的 [維度] 窗格中，檢閱 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 中的 Cube 維度。  
  
    請注意，雖然在資料庫層級只建立了三個維度，如 [方案總管] 中所顯示，但在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 中卻有五個 Cube 維度。 Cube 包含的維度多於資料庫，這是因為以 [日期] 資料庫維度做為 3 個不同日期相關 Cube 維度的基礎，這是基於事實資料表中的不同日期相關事實。 這些日期相關維度也稱為 *「角色扮演維度」*(role playing dimension)。 這 3 個日期相關 Cube 維度可讓使用者根據與每一項產品銷售有關的 3 個不同事實建立 Cube 維度：產品訂單日期、訂單履約的到期日和訂單的送貨日期。 利用對多個 Cube 維度重複使用單一資料庫維度，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 簡化了維度管理，使用更少的磁碟空間，並減少整體處理時間。  
  
4.  在 [Cube 結構] 索引標籤的 [維度] 窗格中，展開 [客戶]，然後按一下 [編輯客戶]，即可在維度設計師中開啟該維度。  
  
    維度設計師包含下列索引標籤：[維度結構]、[屬性關聯性]、[翻譯] 和 [瀏覽器]。 請注意，[維度結構] 索引標籤包含三個窗格：[屬性]、[階層] 和 [資料來源檢視]。 該維度所包含的屬性會顯示在 [屬性] 窗格中。 如需詳細資訊，請參閱[維度屬性 (attribute) 屬性 (property) 參考](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)、[建立使用者定義階層](../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)和[定義屬性關聯性](../analysis-services/multidimensional-models/attribute-relationships-define.md)。  
  
5.  若要切換到 Cube 設計師，可在方案總管中以滑鼠右鍵按一下 [Cube] 節點中的 [Analysis Services 教學課程] Cube，然後按一下 [檢視設計師]。  
  
6.  在 Cube 設計師中，按一下 [維度使用方式] 索引標籤。  
  
    在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的這份檢視中，您會看到 [網際網路銷售] 量值群組所使用的 Cube 維度。 同時，您可以在每個維度和使用該維度的每個量值群組之間定義關聯性類型。  
  
7.  按一下 [資料分割] 索引標籤。  
  
    [Cube 精靈] 會使用不含彙總的多維度線上分析處理 (MOLAP) 儲存模式來定義 Cube 的單一資料分割。 運用 MOLAP，所有分葉層級資料和所有彙總都儲存在 Cube 內，以達到最大效能。 彙總是預先計算的資料彙總，可改進查詢回應時間，因為它在提出問題之前就已備妥答案。 您可以在 [資料分割] 索引標籤上定義其他資料分割、儲存設定和回寫設定。如需詳細資訊，請參閱[資料分割 &#40;Analysis Services - 多維度資料&#41;](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md) 和[彙總和彙總設計](../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)。  
  
8.  按一下 **[瀏覽器]** 索引標籤。  
  
    請注意，您無法瀏覽 Cube，因為它尚未部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。 此時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程專案中的 Cube 只是 Cube 的定義，您可以將它部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。 當您部署和處理 Cube 時，會在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體中建立已定義的物件，並以基礎資料來源的資料來擴展物件。  
  
9. 在方案總管中，以滑鼠右鍵按一下 [Cube] 節點中的 [Analysis Services 教學課程]，然後按一下 [檢視程式碼]。 您可能需要稍等一下。  
  
    [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的 XML 程式碼會顯示在 [[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML]] 索引標籤上。這是開發期間在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體中建立 Cube 時使用的實際程式碼。 如需詳細資訊，請參閱[檢視 Analysis Services 專案的 XML &#40;SSDT&#41;](../analysis-services/multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md)。  
  
10. 關閉 [XML 程式碼] 索引標籤。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[部署 Analysis Services 專案](../analysis-services/lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>另請參閱  
[在維度設計師中瀏覽維度資料](../analysis-services/multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
  
