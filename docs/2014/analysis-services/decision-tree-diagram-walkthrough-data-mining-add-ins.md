---
title: 決策樹圖表逐步解說 （資料採礦增益集） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ef951825144f381ab37a83526ec96321fe43cfec
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66082274"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>決策樹圖表逐步解說 （資料採礦增益集）
  如果您已經建立決策樹模型，就可以在 Visio 中使用 [決策樹] 圖形或 [相依性網路] 圖形來建立自訂的圖表。 本主題說明您可以使用執行的自訂**決策樹**圖形和下列控制項：  
  
-   決策樹圖表的轉譯控制項  
  
     這些選項屬於**決策樹精靈**，在您將圖形放入 Visio 工作區時啟動。  
  
-   **資料採礦配置**工具列  
  
     這些選項會加入至 Visio 工作區以協助您與圖形互動。  
  
## <a name="build-a-decision-tree-diagram"></a>建立決策樹圖表  
 卸除放入 Visio 頁面中，以啟動 [決策樹] 圖形**決策樹 Visio 圖形精靈**並且設定圖表選項。  
  
#### <a name="use-the-decision-tree-wizard"></a>使用決策樹精靈  
  
1.  如果您看不見**Microsoft 資料採礦圖形**中**圖形**清單中，按一下**其他圖形**，選取**開啟樣板**，並開啟從預設安裝位置的範本。  
  
     \<磁碟機 >: \Program 檔案 (x85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  拖曳**決策樹**圖形拖曳至頁面。  
  
3.  在 歡迎使用 頁面上**決策樹 Visio 圖形精靈**，按一下**下一步**。  
  
4.  上**Zdroj Dat**頁面**叢集精靈**，選擇要連接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要視覺化具有模型的伺服器。  
  
5.  選取適當的採礦模型，然後按一下**下一步**。  
  
     此圖表類型支援使用決策樹或線性迴歸演算法所建立的模型。  
  
6.  在 **選取決策樹**頁面上，選擇個別的樹狀目錄以顯示。  
  
     樹狀結構模型會導致您已建立模型; 的特定結果的互動因此，即使您的模型包含多個結果，您就可以一次顯示只有一個樹狀結構。  
  
7.  在 [**選取決策樹**] 對話方塊中，您可以設定下列轉譯選項：  
  
     **最大轉譯深度**  
     您可以使用此選項來控制顯示的節點數目。  
  
     決策樹的深度可能會過高，導致圖表無法容納在頁面上。 請使用此控制項，將焦點放在最左邊的節點上，這些是最重要的節點。  
  
     預設值是三層節點。  
  
     **選取色彩，並顯示其文字值**  
     您可以選擇代表每個結果的色彩。 如果您沒有指定色彩，系統就會使用目前的視訊佈景主題色彩來自動產生色彩。  
  
8.  按一下 **進階**自訂每個決策樹圖表中節點的下列選項。  
  
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
  
     **顯示標頭**  
     加入資料行標題。  
  
     **沒有支援的顯示狀態**  
     讓您顯示遺漏值。  
  
9. 按一下 **完成**建立圖形。  
  
    > [!WARNING]  
    >  在某些環境中，圖表中的連接線可能無法在 Office 2013 中呈現。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 完成後**決策樹 Visio 圖形精靈**，Visio 會以圖形方式顯示導致預測結果的規則，在網頁上建立樹狀圖表。  
  
 您可以繼續使用下列控制項來修改決策樹圖表的圖形：  
  
#### <a name="using-the-decision-tree-option-menus"></a>使用決策樹選項功能表  
  
1.  按一下 **增益集**功能區，然後將其中一個用於處理資料採礦圖表的自訂工具列顯示：  
  
     **版面配置**  
     最佳化樹狀結構的排列方式以符合目前的頁面。  
  
     **調整頁面大小**  
     此控制項適用於先前的 HTML 版本。 請改用 Visio 頁面大小調整控制項。  
  
     **說明**  
     當您選取樹狀結構的節點時，按一下此選項就會顯示有關節點中案例的詳細資料。  
  
2.  使用**重新進行版面配置頁面**在 Visio 中的選項**設計**來試驗不同的樹狀結構配置的功能區。  
  
3.  使用**連接器**選項**設計**索引標籤，變更在樹狀目錄中的節點之間使用的連接器。  
  
4.  使用**取景位置調整及縮放**控制項，在**工作窗格**區域中的 Visio**檢視**功能區中，將焦點放在特定區域的圖表。  
  
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
 [Visio 資料採礦圖表的疑難排解&#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
