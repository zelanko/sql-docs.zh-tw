---
title: 相依性網路圖表逐步解說 （資料採礦增益集） |Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081973"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>相依性網路圖表逐步解說 (資料採礦增益集)
  許多不同類型的資料採礦模型都會使用網路圖形做為探索資料關聯性的方式。 您可以匯入這些模型使用 Visio**相依性網路**圖形，然後繼續自訂並增強配置。 **適用於 Visio 的資料採礦圖形**包含下列自訂控制項，用於處理相依性網路圖表：  
  
-   網路圖形的轉譯控制項  
  
     這些選項屬於精靈的一部分，而這個精靈是在您將圖形放入 Visio 工作區時啟動。  
  
-   **資料採礦配置**工具列  
  
     這些選項會加入至 Visio 工作區以協助您與相依性網路圖形互動。  
  
## <a name="build-a-dependency-network-graph"></a>建立相依性網路圖形  
 您將圖形放入 Visio 頁面中，以啟動放**相依性網路 Visio 圖形精靈**並且設定圖表選項。  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>使用相依性網路 Visio 圖形精靈  
  
1.  如果您看不見**Microsoft 資料採礦圖形**中**圖形**清單中，按一下**其他圖形**，選取**開啟樣板**，並開啟從預設安裝位置的範本。  
  
     \<磁碟機 >: \Program 檔案 (x85) \Microsoft SQL Server 2012 DM Add-ins  
  
2.  拖曳**相依性網路**圖形放入以啟動精靈頁面。 按一下 [下一步] 。  
  
3.  在 歡迎使用 頁面上**相依性網路 Visio 圖形精靈**，按一下**下一步**。  
  
4.  上**Zdroj Dat**頁面**相依性網路 Visio 圖形精靈**，選擇要連接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要視覺化具有模型的伺服器。  
  
5.  選取適當的採礦模型，然後按一下**下一步**。  
  
     若要選取適當模型，您可以檢閱的名稱、 描述、 資料行和中的資料類型**屬性**窗格。  
  
     此圖形支援使用下列演算法所建立的模型：  
  
    -   貝氏機率分類  
  
    -   決策樹  
  
    -   關聯規則  
  
6.  在頁面上，**選取要轉譯的節點**、 自訂圖形的大小，以及選擇性地篩選為僅包含特定節點。  
  
     使用大型資料集，相依性圖形可以變得很大，且包含許多相關的物件，表示為*節點*。 您可以使用此對話方塊來建立僅包含感興趣節點的自訂網路圖形。  
  
     [圖案預留位置]  
  
     **要擷取的節點數目**  
     如果模型包含的節點少於指定的節點數目，這個設定沒有作用。 如果模型包含的節點超過指定的數目，則只會顯示關聯性最強的節點。  
  
     **名稱包含**  
     將這個方塊保留空白，然後按一下綠色箭頭，即可擷取模型中的所有節點。  
  
     或者，輸入字串，然後按一下綠色箭頭，只傳回包含指定字串的節點。  
  
     您可以使用範例資料建立的大部分模型都不會太大，因此在此範例中，請將節點的數目提高至 10，然後按一下綠色箭頭以執行查詢並取得所有節點的清單。  
  
7.  按一下 **進階**設定圖形的陰影和圖案選項。  
  
8.  按一下 [**關閉**以結束**進階**選項] 對話方塊，然後按一下**完成**建立圖形。  
  
## <a name="explore-and-modify-the-finished-diagram"></a>探索和修改完成的圖表  
 在 Visio 建立相依性網路圖形之後，您就可以繼續使用 Visio 中的功能來修改並增強圖形。  
  
 下圖顯示相依性網路圖形的預設配置。  
  
 [圖案預留位置]  
  
1.  使用**取景位置調整及縮放**控制項，在**工作窗格**區域中的 Visio**檢視**功能區中，以專注於一段圖形和圖表中四處移動。  
  
2.  試驗 Visio 所提供的不同圖形配置**重新進行版面配置頁面**選項。  
  
3.  按一下 **增益集**功能區，然後將其中一個用於處理資料採礦圖表的自訂工具列顯示：  
  
     **版面配置**  
     最佳化頁面上的節點配置及變更檢視，以便顯示所有節點。  
  
     **調整頁面大小**  
     變更頁面大小，以便顯示所有節點。  
  
     **邊緣強度**  
     切換整個圖形的邊緣強度顯示。 邊緣是節點之間的連接。 您可以使用滑桿控制項來篩選出關聯性不強的連接。  
  
     **Slider**  
     **滑桿**能夠協助您控制相依性網路圖表中顯示的關聯性的強度。  
  
     圖形中的每個節點代表一個狀態。 箭頭代表兩個狀態之間的轉換以及與轉換相關聯的機率。 若要減少圖形中的節點數目，請將滑動軸向上移。  
  
     若要增加圖形中的節點數目，請將滑動軸向下移。  
  
     **新增項目**  
     會開啟**選取要轉譯的節點**對話方塊，讓您可以選取新的節點加入圖形。  
  
4.  您可以視需要將圖形變得簡單或詳細，並且加入註解，同時維持模型的連接。  
  
     [圖案預留位置]  
  
> [!WARNING]  
>  原本在舊版增益集中提供的反白顯示相依節點和其他捷徑功能表選項無法在 Office 2013 中運作。  
  
## <a name="see-also"></a>另請參閱  
 [Visio 資料採礦圖表的疑難排解&#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
