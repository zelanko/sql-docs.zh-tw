---
title: 決策樹圖表逐步解說（資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shapes, data mining
- diagram, decision tree
- Visio shapes, decision tree
- decision tree [data mining]
ms.assetid: 9566f6a2-c750-4125-ba5e-42c7251a78c7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 755a7f9c8708664dbb3a65c223873cf1dd4e20c8
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528864"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>決策樹圖表逐步解說（資料採礦增益集）
  如果您已經建立決策樹模型，就可以在 Visio 中使用 [決策樹] 圖形或 [相依性網路] 圖形來建立自訂的圖表。 本主題描述您可以使用 [**決策樹**] 圖形和這些控制項來執行的自訂：  
  
-   決策樹圖表的轉譯控制項  
  
     這些選項是當您將圖形放入 Visio 工作區時啟動的**決策樹 Wizard**的一部分。  
  
-   **資料採礦版面**組態工具欄  
  
     這些選項會加入至 Visio 工作區以協助您與圖形互動。  
  
## <a name="build-a-decision-tree-diagram"></a>建立決策樹圖表  
 您可以將 [決策樹] 圖形放到 Visio 頁面上，以啟動**決策樹 Visio 圖形 Wizard**並設定圖表選項。  
  
#### <a name="use-the-decision-tree-wizard"></a>使用決策樹精靈  
  
1.  如果您在 [**圖形**] 清單中看不到 [ **Microsoft 資料採礦圖形**]，請按一下 [**更多圖形**]，選取 [**開啟**樣板]，然後從預設安裝位置開啟範本。  
  
     \<drive>： \Program files （x85） \Microsoft SQL Server 2012 DM 增益集  
  
2.  將 [**決策樹**] 圖形拖曳至頁面上。  
  
3.  在 [**決策樹 Visio 圖形 Wizard]** 的 [歡迎使用] 頁面上，按 **[下一步]**。  
  
4.  在叢集 Wizard 的 [**選取資料來源** **]** 頁面上，選擇 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 具有您想要視覺化之模型的伺服器連接。  
  
5.  選取適當的 [採礦模型]，然後按 **[下一步]**。  
  
     此圖表類型支援使用決策樹或線性迴歸演算法所建立的模型。  
  
6.  在 [**選取決策樹**] 頁面上，選擇要顯示的個別樹狀結構。  
  
     樹狀結構會將導致您所模型化之特定結果的互動模型化。因此，即使您的模型包含多個結果，您一次只能顯示一個樹狀結構。  
  
7.  在 [**選取決策樹**] 對話方塊中，您也可以設定這些轉譯選項：  
  
     **最大轉譯深度**  
     您可以使用此選項來控制顯示的節點數目。  
  
     決策樹的深度可能會過高，導致圖表無法容納在頁面上。 請使用此控制項，將焦點放在最左邊的節點上，這些是最重要的節點。  
  
     預設值是三層節點。  
  
     **選取值的色彩和顯示文字**  
     您可以選擇代表每個結果的色彩。 如果您沒有指定色彩，系統就會使用目前的視訊佈景主題色彩來自動產生色彩。  
  
8.  按一下 [**高級**]，針對決策樹圖表中的每個節點自訂下列選項。  
  
     **陰影變數**和**狀態**  
     選擇您想要顯示在樹狀圖表中的目標結果。  
  
     **顯示長條圖**  
     將圖表加入至每個節點，其中顯示定義該節點的規則。  
  
     **顯示標籤**  
     將資料行名稱加入至長條圖。  
  
     **顯示機率**  
     顯示每個值的機率。  
  
     **顯示支援**  
     顯示每個值的支援。  
  
     **顯示頁尾**  
     加入加總所有顯示值的頁尾。  
  
     **顯示頁首**  
     加入資料行標題。  
  
     **顯示沒有支援的狀態**  
     讓您顯示遺漏值。  
  
9. 按一下 **[完成]** 以建立圖形。  
  
    > [!WARNING]  
    >  在某些環境中，圖表中的連接線可能無法在 Office 2013 中呈現。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 當您完成 [**決策樹 Visio 圖形嚮導]** 之後，Visio 會在頁面上建立一個樹狀圖表，以圖形方式顯示導致預測結果的規則。  
  
 您可以繼續使用下列控制項來修改決策樹圖表的圖形：  
  
#### <a name="using-the-decision-tree-option-menus"></a>使用決策樹選項功能表  
  
1.  按一下 [**增益集**] 功能區，然後顯示用來處理資料採礦圖表的其中一個自訂工具列：  
  
     **配置**  
     最佳化樹狀結構的排列方式以符合目前的頁面。  
  
     **調整頁面大小**  
     此控制項適用於先前的 HTML 版本。 請改用 Visio 頁面大小調整控制項。  
  
     **描述**  
     當您選取樹狀結構的節點時，按一下此選項就會顯示有關節點中案例的詳細資料。  
  
2.  使用 Visio**設計**功能區中的 [**重新配置頁面**] 選項來試驗不同的樹狀結構版面配置。  
  
3.  使用 [**設計**] 索引標籤上的 [**連接器**] 選項，即可變更樹狀結構中節點之間所使用的連接器。  
  
4.  在 Visio **View**功能區的 [工作**窗格]** 區域中，使用 [**平移和縮放**] 控制項，將焦點放在圖表的特定區域。  
  
5.  以滑鼠右鍵按一下樹狀結構中的任何節點，然後從決策樹圖表特有的這些捷徑功能表選項中選擇：  
  
     **修訂頁面配置**  
     在頁面上平均分佈節點，並調整頁面檢視，以便查看所有節點。  
  
     **將子節點移到新頁面**  
     將目前選定節點的子節點移到新頁面。  
  
     **摺疊子節點**  
     隱藏目前選定節點的子節點。  
  
     **展開子節點**  
     顯示目前選定節點的子節點。  
  
## <a name="see-also"></a>另請參閱  
 [針對 Visio 資料採礦圖表進行疑難排解 &#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
