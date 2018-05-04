---
title: 瀏覽已部署的 Cube |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 849c6109-1453-4fe4-a892-c49a982cfadb
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cb6078b0cc6725cb3b62ee6740d8f11437920d3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-3-5---browsing-the-deployed-cube"></a>課程 3-5-瀏覽已部署的 Cube
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在下列工作中，您將瀏覽 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube。 我們的分析會跨多個維度比較量值，因此您將使用 Excel 樞紐分析表瀏覽資料。 使用樞紐分析表可讓您將客戶、日期和產品資訊放在不同的軸上，讓您可以看到跨特定時間週期、客戶人口統計資料和產品線檢視時，[網際網路銷售] 如何變更。  
  
### <a name="to-browse-the-deployed-cube"></a>瀏覽已部署的 Cube  
  
1.  若要切換至 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的 [Cube 設計師]，請在方案總管的 [Cube] 節點中，按兩下 [[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程] Cube。  
  
2.  開啟 [瀏覽器] 索引標籤，然後按一下設計師工具列上的 [重新連接] 按鈕。  
  
3.  按一下 Excel 圖示，啟動 Excel，並使用工作空間資料庫做為資料來源。 出現啟用連接的提示時，按一下 [啟用]。  
  
4.  在樞紐分析表欄位清單中，展開 [網際網路銷售]，然後將 [銷售量] 量值拖曳至 [值] 區域中。  
  
5.  在樞紐分析表欄位清單中，展開 [產品]。  
  
6.  將 [產品型號線] 使用者階層拖曳至 [資料行] 區域。  
  
7.  在樞紐分析表欄位清單中，依序展開 [客戶] 和 [位置]，然後從 [客戶] 維度的 [位置] 顯示資料夾，將 [客戶地理位置] 階層拖曳到 [資料列] 區域。  
  
8.  在樞紐分析表欄位清單中，展開 [訂購日期]，然後將 [Order Date.Calendar Date] 階層拖曳到 [報表篩選] 區域。  
  
9. 按一下資料窗格中 [Order Date.Calendar Date] 篩選右邊的箭頭、清除 [(全部)] 層級的核取方塊、依序展開 [2006]、[H1 CY 2006] 和 [Q1 CY 2006]、選取 [February 2006] 的核取方塊，然後按一下 [確定]。  
  
    此時會出現按區域的網際網路銷售量和 2006 年 2 月的當月產品線，如下圖所示。  
  
    ![依區域和產品線的網際網路銷售額](../analysis-services/media/l3-cube-browser-finish.gif "依地區和產品線的網際網路銷售額")  
  
## <a name="next-lesson"></a>下一課  
[第 4 課： 定義進階的屬性和維度屬性](../analysis-services/lesson-4-defining-advanced-attribute-and-dimension-properties.md)  
  
  
  
