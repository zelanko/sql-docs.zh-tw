---
title: "瀏覽 Cube |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: 3819946e-d3fa-4c1d-afe3-599c938b1b2e
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 00dee701e3bea7e30924352e136c6202d6a10ced
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-6---browsing-the-cube"></a>課程 2-6-瀏覽 Cube
部署 Cube 之後，您就可以在 [Cube 設計師] 的 [瀏覽器] 索引標籤上檢視 Cube 資料，以及在 [維度設計師] 的 [瀏覽器] 索引標籤上檢視維度資料。 瀏覽 Cube 和維度資料是累加地檢查工作的一種方式。 您可以在物件經處理之後，驗證對屬性、關聯性和其他物件所做的細微變更是否達到期望的效果。 由於 [瀏覽器] 索引標籤用於檢視 Cube 和維度資料，因此該索引標籤會根據您要瀏覽的物件，提供不同的功能。  
  
若是維度，[瀏覽器] 索引標籤會提供一種方式，以檢視成員或導覽一直到分葉節點的階層。 假設您已經將翻譯加入至模型中，便可以不同語言瀏覽維度資料。  
  
若是 Cube，[瀏覽器] 索引標籤則會提供兩種瀏覽資料的方法。 您可以使用內建的 MDX 查詢設計工具，建立從多維度資料庫傳回扁平化資料列集的查詢。 或者，您可以使用 Excel 捷徑。 如果您從 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中啟動 Excel，當 Excel 開啟時，工作表中已經有一個樞紐分析表，以及一個連至模型工作空間資料庫之預先定義的連接。  
  
Excel 通常會提供一個比較好的瀏覽經驗，因為您可以透過互動方式瀏覽 Cube 資料，並使用水平和垂直軸分析資料中的關聯性。 相較之下，MDX 查詢設計工具限制為單一軸。 此外，由於資料列集經過扁平化，因此您不需要使用 Excel 樞紐分析表所提供的向下鑽研功能。 隨著您在 Cube 中加入更多維度和階層 (您將在後續的課程中進行)，Excel 將是瀏覽資料慣用的解決方案。  
  
### <a name="to-browse-the-deployed-cube"></a>瀏覽已部署的 Cube  
  
1.  針對 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [產品] 維度，切換至 [維度設計師]。 若要這樣做，請在方案總管的 [維度] 節點中，按兩下 [產品] 維度。  
  
2.  按一下 [瀏覽器] 索引標籤，即可顯示 [產品金鑰] 屬性階層的 [全部] 成員。 在第 3 課，您將定義 [產品] 維度的使用者階層，以便瀏覽此維度。  
  
3.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，切換至 [Cube 設計師]。 若要這樣做，請在方案總管的 [Cube] 節點中，按兩下 [Analysis Services 教學課程] Cube。  
  
4.  選取 [瀏覽器] 索引標籤，然後按一下設計師工具列上的重新連接圖示。  
  
    設計師的左窗格會顯示 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 中的物件。 [瀏覽器] 索引標籤的右側具有兩個窗格：上面的窗格是 [篩選] 窗格，而下面的窗格是 [資料] 窗格。 在後續課程中，您將使用 Cube 瀏覽器來進行分析。  
  
## <a name="next-lesson"></a>下一課  
[第 3 課：修改量值、屬性和階層](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>另請參閱  
[MDX 查詢編輯器 &#40;Analysis Services - 多維度資料&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)  
  
  
  
