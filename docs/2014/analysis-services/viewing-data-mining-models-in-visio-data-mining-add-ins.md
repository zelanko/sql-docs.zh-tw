---
title: 檢視資料採礦模型在 Visio 中 （資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagram, modifying
- templates [Visio]
- shapes, data mining
- diagram
ms.assetid: 5841adea-6650-4fae-8526-26af33edbede
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9dbb4e78685982dc3b7cd981fc6df6db9bf40a13
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259354"
---
# <a name="viewing-data-mining-models-in-visio-data-mining-add-ins"></a>在 Visio 中檢視資料採礦模型 (資料採礦增益集)
  資料採礦的 Visio 圖形可讓您連接到伺服器並建立代表現有資料採礦模型的圖表。 然後，您可以使用 Visio 控制項來自訂圖表，但是也可以向下鑽研資料、公開部分基礎統計資料，以及使用基礎模型。  
  
## <a name="building-a-model-diagram"></a>建立模型圖表  
 當您開啟包含資料採礦的 Visio 圖形的檔案時**圖形**窗格會顯示下列圖形。  
  
 如果您在開啟 Visio 時沒有看見資料採礦圖形，可以從安裝資料夾開啟範本檔案。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 若要使用圖形，請將它拖曳至頁面。 每個圖形會開啟不同精靈，以協助您選取來源資料、設定特定圖表類型的選項，以及指定陰影和其他顯示選項。  
  
 下表列出您可以搭配每一種圖表類型使用的模型類型。  
  
|Visio 圖形|支援的模型|  
|-----------------|----------------------|  
|決策樹|請針對以決策樹或線性迴歸演算法為基礎的模型使用此圖形。|  
|相依性網路|請針對以下列任一個演算法為基礎的模型使用此圖形：貝氏機率分類、決策樹或關聯規則。|  
|叢集|請針對以叢集演算法為基礎的模型使用此圖形。|  
  
 根據採礦模型中的資料類型，精靈可能會提供不同選項。 例如，包含連續數字之資料行的視覺效果方式與類別變數有所不同。  
  
## <a name="working-with-completed-shapes"></a>使用已完成圖形  
 圖表完成之後，您可以用它來瀏覽資料採礦模型或增強圖表以用於簡報中。  
  
### <a name="visio-menus"></a>Visio 功能表  
 Visio 提供了各種轉譯控制項、佈景主題和捷徑功能表來協助您增強圖表。  
  
-   使用 Visio 佈景主題來更改圖表色彩。  
  
-   變更連接線或圖表配置。  
  
### <a name="data-mining-menus"></a>資料採礦功能表  
 這些工具列和功能表項目都是由每個圖形或模型類型專用的增益集提供的。  
  
-   每個圖表類型都有圖形的快速鍵功能表，可讓您存取特殊選項。 雖然這個功能表中的許多選項是所有 Visio 圖形共有的，但有些選項卻是資料採礦範本特有的選項。  
  
     例如，在決策樹圖表中，您可以按一下個別節點，然後摺疊子節點讓圖表更簡單，或將子節點移至另一個頁面。  
  
-   因為圖形已繫結至模型資料，所以您也可以使用圖表來進行一些瀏覽動作：  
  
     篩選顯示的節點，或者變更樹狀的層級或圖形的深度。  
  
     放大特定部分、搜尋包含特定屬性的節點，或依據邊緣 (機率) 來篩選相依性圖形。  
  
## <a name="walkthroughs"></a>逐步解說  
 如需如何使用及解譯已完成圖表的範例，請參閱以下這些主題：  
  
 [叢集圖表逐步解說](cluster-diagram-walkthrough-data-mining-add-ins.md)  
  
 [相依性網路圖表逐步解說](dependency-network-diagram-walkthrough-data-mining-add-ins.md)  
  
 [決策樹圖表逐步解說](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽模型，在 Excel 中的&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
