---
title: "修改量值 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 350fadc471d30f79b8b1e6b1e8d63cc507f1d484
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-3-1---modifying-measures"></a>課程 3-1-修改量值
您可以使用 [FormatString] 屬性來定義格式設定，以便控制向使用者顯示量值的方式。 在這項工作中，您在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 中指定貨幣和百分比量值的格式化屬性。  
  
### <a name="to-modify-the-measures-of-the-cube"></a>若要修改 Cube 的量值  
  
1.  針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube，切換到 [Cube 設計師] 的 [Cube 結構] 索引標籤，並展開 [量值] 窗格中的 [網際網路銷售] 量值群組，然後以滑鼠右鍵按一下 [訂購數量]，再按一下 [屬性]。  
  
2.  在 [屬性] 視窗中，按一下 [自動隱藏] 圖釘圖示來固定開啟 [屬性] 視窗。  
  
    當 [屬性] 視窗保持開啟時，要在 Cube 中變更數個項目的屬性會更加容易。  
  
3.  在 [屬性] 視窗中，按一下 [FormatString] 清單，然後輸入 **#,#**。  
  
4.  在 [Cube 結構] 索引標籤的工具列上，按一下左側的 [顯示量值方格] 圖示。  
  
    方格檢視可讓您同時選取多個量值。  
  
5.  選取下列量值。 您可以在按住 CTRL 鍵的同時，按一下每個量值，藉以選取多個量值：  
  
    -   **單價**  
  
    -   **擴充量**  
  
    -   **折扣量**  
  
    -   **產品標準成本**  
  
    -   **產品總成本**  
  
    -   **銷售量**  
  
    -   **稅額**  
  
    -   **Freight**  
  
6.  在 [屬性] 視窗的 [FormatString] 清單中，選取 [貨幣]。  
  
7.  在 [屬性] 視窗 (標題列正下方) 頂端的下拉式清單中，選取 [單價折扣百分比] 量值，然後選取 [FormatString] 清單中的 [百分比]。  
  
8.  在 [屬性] 視窗中，將 [單價折扣百分比] 量值的 [名稱] 屬性變更為 [單價折扣百分比]。  
  
9. 在 [量值] 窗格中，按一下 [稅額]，並將這個量值的名稱變更為 [稅額]。  
  
10. 在 [屬性] 視窗中，按一下 [自動隱藏] 圖示隱藏 [屬性] 視窗，然後按一下 [Cube 結構] 索引標籤的工具列上的 [顯示量值樹狀目錄]。  
  
11. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[修改 [客戶] 維度](../analysis-services/lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>另請參閱  
[定義資料庫維度](../analysis-services/multidimensional-models/define-database-dimensions.md)  
[設定量值屬性](../analysis-services/multidimensional-models/configure-measure-properties.md)  
  
  
  

