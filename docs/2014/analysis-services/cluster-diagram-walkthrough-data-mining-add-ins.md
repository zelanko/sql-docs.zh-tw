---
title: 叢集圖表逐步解說（資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc2df250b0728934f258c8217d29adfb91e66ff5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087906"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>叢集圖表逐步解說 (資料採礦增益集)
  建立群集模型之後，您可以**使用 [叢集] 圖形將它**匯入 Visio，然後繼續自訂並增強配置。 **適用于 Visio 的資料採礦圖形**包含下列自訂控制項，可用來處理資料採礦圖表：  
  
-   叢集圖表的轉譯控制項  
  
     這些選項是在您將圖形放入 Visio 工作區時啟動的叢集**Wizard**的一部分。  
  
-   **資料採礦版面**組態工具欄  
  
     這些選項會加入至 Visio 工作區以協助您與資料採礦圖形互動。 這些選項會因您所使用的資料採礦模型類型而異。  
  
## <a name="build-a-cluster-diagram"></a>建立叢集圖表  
 這個逐步解說會示範如何在 Visio 中建立並自訂叢集圖表。  
  
 若要依照步驟進行，您應該事先備妥叢集模型。 如果您沒有模型，請使用 [叢集[] wizard &#40;適用于 Excel 的資料採礦增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md) Wizard，並使用範例活頁簿中的訓練資料集，並使用所有預設值來建立模型。  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>使用叢集 Visio 圖形精靈  
  
1.  如果您在 [**圖形**] 清單中看不到 [ **Microsoft 資料採礦圖形**]，請按一下 [**更多圖形**]，選取 [**開啟**樣板]，然後從預設安裝位置開啟範本。  
  
     \<磁片磁碟機>： \Program files\Microsoft SQL Server 2012 DM 增益集  
  
2.  **將 [叢集] 圖形拖曳**至頁面上。  
  
3.  在 [叢集**Visio 圖形 Wizard]** 的 [歡迎使用] 頁面上，按 **[下一步]**。  
  
4.  在叢集 Wizard 的 [**選取資料來源** **]** 頁面上，選擇包含您想要[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]視覺化之資料採礦模型的伺服器連接。  
  
5.  選取適當的 [採礦模型]，然後按 **[下一步]**。  
  
     若要確定您選擇群集模型，請檢查 [**屬性**] 窗格中的描述。  
  
6.  如果連線成功，在 [叢集**圖表的選項**] 頁面上，您可以決定要在 Visio 簡報中包含哪種類型的群集圖表：  
  
     **只顯示群集形狀**  
     這個選項會建立簡單的叢集圖表，其中每個叢集都由矩形或您所選擇的其他圖形代表。  
  
     **顯示有特性圖表的群集**  
     這個選項所建立的圖表與上述選項相同，但是圖形內部是描述叢集特性的長條圖。  
  
     ![Visio 的叢集特性圖表範例](media/dm13-visio-cluster-samplecharshape.gif "Visio 的叢集特性圖表範例")  
  
     **顯示有辨識圖表的群集**  
     這個選項所建立的圖表與叢集圖表相同，但是改為列出目前叢集與其他叢集區別最強烈的特性。  
  
     您可以在精靈建立圖表之後，以滑鼠右鍵按一下叢集並選取新的圖表類型，藉以切換成其他圖表類型。 現在，請選擇 [**顯示具有特性圖表的**叢集] 選項。  
  
7.  將 [**圖表中的資料列數目**] 選項保留為5。  
  
     此選項不會變更模型中的群集數目;它只會限制可以顯示為每個叢集之功能的屬性數目。  
  
     不過，此選項會做為圖表資料的篩選，因此您稍後無法增加專案數。  
  
8.  按一下 [進階]****。  
  
     [叢集**選項**] 對話方塊可讓您自訂圖表中所使用之圖形的視覺外觀。 您可以變更用於圖形的色彩，以及用於叢集的圖形。  
  
     [**陰影變數**] 控制項無法在 Office 2013 中運作。  
  
     ![按一下 [進階] 選擇形狀色彩](media/dm13-visio-clusteroptions-advanced.gif "按一下 [進階] 選擇形狀色彩")  
  
     **秘訣：** 有些色彩稍後可以使用 Visio 主題和圖形編輯控制項來改變。 不過，Visio 佈景主題也會覆寫其中部分色彩選擇，因此我們建議您從預設色彩開始，逐漸套用變更。  
  
9. 按一下 **[完成]** 以建立圖形。  
  
     此精靈會從資料採礦模型中擷取資訊、轉譯圖形，並在每個叢集中填入屬性和值。  
  
     ![相依性網路](media/dm13-visiodepnet-defaultgraph.gif "相依性網路")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 在圖表完成之後，您可以繼續使用 Visio 控制項來自訂外觀，如下列範例所示。  
  
 ![使用 Visio 自訂的叢集圖表](media/dm13-visio-clustercomplete1.gif "使用 Visio 自訂的叢集圖表")  
  
 所有基本叢集圖形都由精靈產生。請使用下列工具來更新並個人化圖表：  
  
1.  拖曳 [叢集**選項**] 控制項中的滑杆，以篩選掉較弱的關聯性並簡化圖表。  
  
2.  使用 [Visio**重新配置頁面**] 選項來試驗不同的叢集版面配置。  
  
3.  使用 [**設計**] 索引標籤上的 [**連接器**] 選項來變更連接器樣式，使線條不會跨越叢集。  
  
4.  按一下 [**增益集**] 功能區，然後顯示用來處理資料採礦圖表的其中一個自訂工具列：  
  
     **配置**  
     最佳化叢集的排列方式以符合目前的頁面。  
  
     **調整頁面大小**  
     此控制項適用於先前的 HTML 版本。 請改用 Visio 頁面大小調整控制項。  
  
     **描述**  
     如果選取了叢集，按一下這個選項就會顯示有關叢集的詳細資料。  
  
     ![按一下 [描述] 取得叢集的詳細資料](media/dm13-visio-cluster-description-control.gif "按一下 [描述] 取得叢集的詳細資料")  
  
     **邊緣強度**  
     在連接叢集的線條上顯示信心分數。  
  
     不過，如果您套用精靈產生之預設格式設定以外的任何特殊格式設定，包括部分背景，可能就不會顯示這些數字。  
  
     **滑桿**  
     篩選叢集之間的線條。 將滑動軸向上移就會移除最重要關聯以外的所有關聯。  
  
     **陰影**  
     此控制項無法在 Office 2013 中運作。  
  
5.  您可以使用 [Visio View] 功能區的 [工作**窗格]** 區域中的 [移動**流覽****和縮放**] 控制項，將焦點放在一組叢集上，然後在圖表中四處移動。  
  
6.  以滑鼠右鍵按一下任何叢集，即可查看該叢集圖形特有的選項：  
  
    -   變更圖表樣式。  
  
    -   加入叢集特性圖表。  
  
    -   加入叢集辨識圖表。  
  
## <a name="see-also"></a>另請參閱  
 [針對 Visio 資料採礦圖表進行疑難排解 &#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
