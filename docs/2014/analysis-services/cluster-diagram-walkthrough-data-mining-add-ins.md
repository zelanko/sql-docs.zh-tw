---
title: 叢集圖表逐步解說 （資料採礦增益集） |Microsoft Docs
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
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 808accf81389f97d2dff9383fe4c3fbe9d86068d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177255"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>叢集圖表逐步解說 (資料採礦增益集)
  您已建立叢集模型之後，您可以匯入它使用 Visio**叢集**圖形，然後繼續自訂並增強配置。 **適用於 Visio 的資料採礦圖形**包含下列用於處理資料採礦圖表的自訂控制項：  
  
-   叢集圖表的轉譯控制項  
  
     這些選項屬於**叢集精靈**，在您將圖形放入 Visio 工作區時啟動。  
  
-   **資料採礦配置**工具列  
  
     這些選項會加入至 Visio 工作區以協助您與資料採礦圖形互動。 這些選項會因您所使用的資料採礦模型類型而異。  
  
## <a name="build-a-cluster-diagram"></a>建立叢集圖表  
 這個逐步解說會示範如何在 Visio 中建立並自訂叢集圖表。  
  
 若要依照步驟進行，您應該事先備妥叢集模型。 如果您沒有模型，使用[叢集精靈&#40;適用於 Excel 的資料採礦增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)精靈並使用定型資料集的活頁簿中，使用所有預設值建立模型。  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>使用叢集 Visio 圖形精靈  
  
1.  如果您看不見**Microsoft 資料採礦圖形**中**圖形**清單中，按一下**其他圖形**，選取**開啟樣板**，並開啟從預設安裝位置的範本。  
  
     \<磁碟機 >: files\microsoft SQL Server 2012 DM Add-ins  
  
2.  拖曳**叢集**圖形拖曳至頁面。  
  
3.  在 歡迎使用 頁面上**叢集 Visio 圖形精靈**，按一下**下一步**。  
  
4.  上**Zdroj Dat**頁面**叢集精靈**，選擇要連接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要以視覺化方式檢視包含的資料採礦模型的伺服器。  
  
5.  選取適當的採礦模型，然後按一下**下一步**。  
  
     若要確定您選擇叢集模型中，檢閱中的說明**屬性**窗格。  
  
6.  如果連線成功，在頁面上，**叢集圖表的選項**，決定要包含在 Visio 簡報中的叢集圖表的類型：  
  
     **只顯示群集形狀**  
     這個選項會建立簡單的叢集圖表，其中每個叢集都由矩形或您所選擇的其他圖形代表。  
  
     **顯示有特性圖表的群集**  
     這個選項所建立的圖表與上述選項相同，但是圖形內部是描述叢集特性的長條圖。  
  
     ![在 Visio 中的叢集特性圖表的範例](media/dm13-visio-cluster-samplecharshape.gif "在 Visio 中的叢集特性圖表的範例")  
  
     **顯示有辨識圖表的群集**  
     這個選項所建立的圖表與叢集圖表相同，但是改為列出目前叢集與其他叢集區別最強烈的特性。  
  
     您可以在精靈建立圖表之後，以滑鼠右鍵按一下叢集並選取新的圖表類型，藉以切換成其他圖表類型。 現在，請選擇選項，**顯示有特性圖表的群集**。  
  
7.  保留選項，**圖表中的資料列數目**，為 5。  
  
     這個選項不會變更模型中的叢集數目，只會限制可顯示成每個叢集之特性的屬性數目而已。  
  
     不過，此選項會做為圖表資料的篩選，因此您之後將無法增加項目數。  
  
8.  按一下 **[進階]**。  
  
     **叢集選項**對話方塊可讓您可讓您自訂圖表中使用之圖形的視覺外觀。 您可以變更用於圖形的色彩，以及用於叢集的圖形。  
  
     **陰影變數**控制 Office 2013 中無法運作。  
  
     ![按一下 [進階] 選擇形狀色彩](media/dm13-visio-clusteroptions-advanced.gif "按一下 [進階] 選擇形狀色彩")  
  
     **提示：** 可以稍後再更改部分色彩，使用 Visio 佈景主題和圖形編輯控制項。 不過，Visio 佈景主題也會覆寫其中部分色彩選擇，因此我們建議您從預設色彩開始，逐漸套用變更。  
  
9. 按一下 **完成**建立圖形。  
  
     此精靈會從資料採礦模型中擷取資訊、轉譯圖形，並在每個叢集中填入屬性和值。  
  
     ![相依性網路](media/dm13-visiodepnet-defaultgraph.gif "相依性網路")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 在圖表完成之後，您可以繼續使用 Visio 控制項來自訂外觀，如下列範例所示。  
  
 ![使用 Visio 來自訂叢集圖表](media/dm13-visio-clustercomplete1.gif "使用 Visio 來自訂叢集圖表")  
  
 所有基本叢集圖形都由精靈產生。請使用下列工具來更新並個人化圖表：  
  
1.  拖曳滑桿**叢集選項**控制項，來篩選出較弱的關聯性，並簡化圖表。  
  
2.  使用 Visio**重新進行版面配置頁面**選項來試驗不同的叢集配置。  
  
3.  使用**連接器**選項**設計**索引標籤來變更連接線樣式，避免讓線條橫跨叢集。  
  
4.  按一下 **增益集**功能區，然後將其中一個用於處理資料採礦圖表的自訂工具列顯示：  
  
     **版面配置**  
     最佳化叢集的排列方式以符合目前的頁面。  
  
     **調整頁面大小**  
     此控制項適用於先前的 HTML 版本。 請改用 Visio 頁面大小調整控制項。  
  
     **說明**  
     如果選取了叢集，按一下這個選項就會顯示有關叢集的詳細資料。  
  
     ![按一下 [描述]，以取得詳細的叢集](media/dm13-visio-cluster-description-control.gif "按一下 [描述]，以取得有關叢集的詳細資料")  
  
     **邊緣強度**  
     在連接叢集的線條上顯示信心分數。  
  
     不過，如果您套用精靈產生之預設格式設定以外的任何特殊格式設定，包括部分背景，可能就不會顯示這些數字。  
  
     **滑桿**  
     篩選叢集之間的線條。 將滑動軸向上移就會移除最重要關聯以外的所有關聯。  
  
     **陰影**  
     此控制項無法在 Office 2013 中運作。  
  
5.  使用**取景位置調整及縮放**控制項，在**工作窗格**區域中的 Visio**檢視**功能區中，以專注於一組叢集，並在圖表中四處移動。  
  
6.  以滑鼠右鍵按一下任何叢集，即可查看該叢集圖形特有的選項：  
  
    -   變更圖表樣式。  
  
    -   加入叢集特性圖表。  
  
    -   加入叢集辨識圖表。  
  
## <a name="see-also"></a>另請參閱  
 [Visio 資料採礦圖表的疑難排解&#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
