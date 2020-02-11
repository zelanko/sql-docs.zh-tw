---
title: 相依性網狀圖表逐步解說（資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db069b243a0d06c142651ab4dcadd68e1e06657f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081973"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>相依性網路圖表逐步解說 (資料採礦增益集)
  許多不同類型的資料採礦模型都會使用網路圖形做為探索資料關聯性的方式。 您可以使用 [相依性**網路**] 圖形將這些模型匯入 Visio，然後繼續自訂並增強版面配置。 **適用于 Visio 的資料採礦圖形**包含下列用來處理相依性網狀圖表的自訂控制項：  
  
-   網路圖形的轉譯控制項  
  
     這些選項屬於精靈的一部分，而這個精靈是在您將圖形放入 Visio 工作區時啟動。  
  
-   **資料採礦版面**組態工具欄  
  
     這些選項會加入至 Visio 工作區以協助您與相依性網路圖形互動。  
  
## <a name="build-a-dependency-network-graph"></a>建立相依性網路圖形  
 您可以將圖形放到 Visio 頁面上，以啟動相依性**網路 Visio 圖形 Wizard**並設定圖表選項。  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>使用相依性網路 Visio 圖形精靈  
  
1.  如果您在 [**圖形**] 清單中看不到 [ **Microsoft 資料採礦圖形**]，請按一下 [**更多圖形**]，選取 [**開啟**樣板]，然後從預設安裝位置開啟範本。  
  
     \<磁片磁碟機>： \Program files （x85） \Microsoft SQL Server 2012 DM 增益集  
  
2.  將 [相依性**網路**] 圖形拖曳至頁面上，以啟動精靈。 按 [下一步]  。  
  
3.  在相依性**網路 Visio 圖形 Wizard**的 [歡迎使用] 頁面上，按 **[下一步]**。  
  
4.  在 [相依性**網路 Visio 圖形 Wizard]** 的 [**選取資料來源**] 頁面上，選擇具有[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要視覺化之模型的伺服器連接。  
  
5.  選取適當的 [採礦模型]，然後按 **[下一步]**。  
  
     若要選取適當的模型，您可以在 [**屬性**] 窗格中，檢查名稱、描述、資料行和資料類型。  
  
     此圖形支援使用下列演算法所建立的模型：  
  
    -   貝氏機率分類  
  
    -   決策樹  
  
    -   關聯規則  
  
6.  在頁面上，**選取要**轉譯的節點、自訂圖形的大小，並選擇性地篩選成隻包含特定的節點。  
  
     使用大型資料集時，相依性圖形可能會變得很龐大，而且包含許多相關物件，以*節點*表示。 您可以使用此對話方塊來建立僅包含感興趣節點的自訂網路圖形。  
  
     [藝術預留位置]  
  
     **要提取的節點數目**  
     如果模型包含的節點少於指定的節點數目，這個設定沒有作用。 如果模型包含的節點超過指定的數目，則只會顯示關聯性最強的節點。  
  
     **名稱包含**  
     將這個方塊保留空白，然後按一下綠色箭頭，即可擷取模型中的所有節點。  
  
     或者，輸入字串，然後按一下綠色箭頭，只傳回包含指定字串的節點。  
  
     您可以使用範例資料建立的大部分模型都不會太大，因此在此範例中，請將節點的數目提高至 10，然後按一下綠色箭頭以執行查詢並取得所有節點的清單。  
  
7.  按一下 [ **Advanced** ] 以設定圖形的陰影和形狀選項。  
  
8.  按一下 [關閉] 以**結束**[ **Advanced** options] 對話方塊，然後按一下 **[完成**] 以建立圖形。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 在 Visio 建立相依性網路圖形之後，您就可以繼續使用 Visio 中的功能來修改並增強圖形。  
  
 下圖顯示相依性網路圖形的預設配置。  
  
 [藝術預留位置]  
  
1.  使用 [工作**窗格]** 功能區的 [移動**流覽****和縮放**] 控制項，將焦點放在圖形的某個區段上，然後在圖表中四處移動。  
  
2.  使用 [Visio**重新配置頁面**] 選項所提供的不同圖形版面配置進行實驗。  
  
3.  按一下 [**增益集**] 功能區，然後顯示用來處理資料採礦圖表的其中一個自訂工具列：  
  
     **版面配置**  
     最佳化頁面上的節點配置及變更檢視，以便顯示所有節點。  
  
     **調整頁面大小**  
     變更頁面大小，以便顯示所有節點。  
  
     **邊緣強度**  
     切換整個圖形的邊緣強度顯示。 邊緣是節點之間的連接。 您可以使用滑桿控制項來篩選出關聯性不強的連接。  
  
     **滑桿**  
     **滑杆**可協助您控制相依性網狀圖表中顯示之關聯性的強度。  
  
     圖形中的每個節點代表一個狀態。 箭頭代表兩個狀態之間的轉換以及與轉換相關聯的機率。 若要減少圖形中的節點數目，請將滑動軸向上移。  
  
     若要增加圖形中的節點數目，請將滑動軸向下移。  
  
     **新增專案**  
     開啟 [**選取要**轉譯的節點] 對話方塊，讓您可以選取要加入至圖形的新節點。  
  
4.  您可以視需要將圖形變得簡單或詳細，並且加入註解，同時維持模型的連接。  
  
     [圖案預留位置]  
  
> [!WARNING]  
>  原本在舊版增益集中提供的反白顯示相依節點和其他捷徑功能表選項無法在 Office 2013 中運作。  
  
## <a name="see-also"></a>另請參閱  
 [針對 Visio 資料採礦圖表進行疑難排解 &#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
