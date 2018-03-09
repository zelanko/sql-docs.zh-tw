---
title: "檢視 Cube 結構描述 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 82fc715c-e08e-447d-8fc8-9c9005f145f0
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 25343dab0a818aa86f0a3a2f5080204602cc1f38
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="view-the-cube-schema"></a>檢視 Cube 結構描述
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
**[Cube 設計師]** 之 **[Cube 結構]** 索引標籤的 **[資料來源檢視]** 窗格顯示 Cube 結構描述。 結構描述是一組衍生 Cube 量值和維度的來源資料表。 每一個 Cube 結構描述是由一個或多個事實資料表及一個或多個維度資料表所組成，Cube 中的量值和維度會以這些資料表為基礎。  
  
 **[Cube 結構]** 索引標籤的 **[資料來源檢視]** 窗格顯示做為 Cube 基礎之資料來源檢視的圖表。 此圖表是資料來源檢視主要圖表的子集。 您可以隱藏及顯示 **[資料來源檢視]** 窗格中的資料表，以及檢視任何現有的圖表。 但是，您無法變更基礎結構描述 (例如將新關聯性或具名查詢加入基礎結構描述)。 若要變更結構描述，請使用資料來源檢視設計工具。  
  
 當您建立 Cube 時，顯示在 **[Cube 結構]** 索引標籤之 **[資料來源檢視]** 窗格中的圖表，一開始會與專案或資料庫之資料來源檢視中的 **[顯示所有資料表]** 圖表相同。 您可以使用資料來源檢視中的任何現有圖表來取代此圖表，並在 **[資料來源檢視]** 窗格中進行調整。  
  
 當您在 **[Cube 設計師]**中使用圖表時， **[資料來源檢視]** 功能表會提供作用於索引標籤或索引標籤中任何所選物件的命令。 您也可以在圖表背景或圖表中的任何物件上按一下滑鼠右鍵，以使用作用於圖表或所選物件的命令。 您可以：  
  
-   在圖表和樹狀格式之間進行切換。  
  
-   排列、尋找、顯示及隱藏資料表。  
  
-   顯示易記名稱。  
  
-   切換配置。  
  
-   變更縮放比例。  
  
-   檢視屬性。  
  
 此外，您可以執行下表中所列的動作：  
  
|若要|執行方式|  
|--------|-------------|  
|使用 Cube 之資料來源檢視中的圖表|在 **[資料來源檢視]** 功能表上，指向 **[複製圖表來源]**，然後按一下您要使用的資料來源檢視圖表。<br /><br /> - 或 -<br /><br /> 以滑鼠右鍵按一下 [資料來源檢視] 窗格的背景，然後指向 [複製圖表來源]，再按一下資料來源檢視中您想要的圖表。 此方法會建立單獨的圖表複本，讓您在 **[Cube 產生器]** 索引標籤上所做的任何變更不會出現在原始圖表中。|  
|僅顯示 Cube 所使用的資料表|在 **[資料來源檢視]** 功能表上，按一下 **[僅顯示使用過的資料表]**。<br /><br /> - 或 -<br /><br /> 以滑鼠右鍵按一下 [資料來源檢視] 窗格的背景，然後按一下 [僅顯示使用過的資料表]。|  
|編輯資料來源檢視結構描述|在 **[資料來源檢視]** 功能表上，按一下 **[編輯資料來源檢視]**。<br /><br /> - 或 -<br /><br /> 以滑鼠右鍵按一下 [資料來源檢視] 窗格的背景，然後按一下 [編輯資料來源檢視]。|  
  
  
