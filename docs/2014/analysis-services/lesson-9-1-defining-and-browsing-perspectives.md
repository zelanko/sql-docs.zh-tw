---
title: 定義和瀏覽檢視方塊 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 766004b9-6578-4914-a445-6f44843a5fb0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a599a1ad2b4a2da7b3078b42b87f859b0f6bdfd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728240"
---
# <a name="defining-and-browsing-perspectives"></a>定義和瀏覽檢視方塊
  檢視方塊可以針對特定的用途，簡化 Cube 的檢視。 根據預設，使用者可以看到 Cube 中他們擁有權限的所有元素。 當使用者檢視整個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube 時，他們所檢視的就是該 Cube 的預設檢視方塊。 整個 Cube 的檢視可能非常複雜，讓使用者難以瀏覽，尤其有的使用者只需要與一小部分的 Cube 互動，即可滿足他們的商業智慧和報告需求。  
  
 若要簡化 Cube 明顯的複雜性，您可以建立稱為 *「檢視方塊」*(Perspective) 的可檢視 Cube 子集，它只會讓使用者看到 Cube 中部分的量值群組、量值、維度、屬性、階層、關鍵效能指標 (KPI)、動作以及導出成員。 這對於使用針對舊版 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]所撰寫的用戶端應用程式特別有用。 例如，雖然這些用戶端沒有顯示資料夾或檢視方塊的概念，但是對於舊版的用戶端而言，檢視方塊就像是 Cube 一樣。 如需詳細資訊，請參閱 [檢視方塊](multidimensional-models-olap-logical-cube-objects/perspectives.md)和 [多維度模型中的檢視方塊](multidimensional-models/perspectives-in-multidimensional-models.md)。  
  
> [!NOTE]  
>  雖然檢視方塊不是安全性機制，不過這個工具卻可以提供更理想的使用者經驗。 檢視方塊的所有安全性，都是繼承自基礎 Cube。  
  
 在這個主題的工作中，您要定義幾個不同的檢視方塊，然後透過每一個新檢視方塊來瀏覽 Cube。  
  
## <a name="defining-an-internet-sales-perspective"></a>定義網際網路銷售檢視方塊  
  
1.  開啟 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的 [Cube 設計師]，然後按一下 [檢視方塊] 索引標籤。  
  
     所有物件和其物件類型都會顯示在 [檢視方塊] 窗格中，如下圖所示。  
  
     ![Cube 設計師的檢視方塊窗格](../../2014/tutorials/media/l9-perspectives-1.gif "Cube 設計師的檢視方塊窗格")  
  
2.  在 [檢視方塊] 索引標籤的工具列上，按一下 [新增檢視方塊] 按鈕。  
  
     新的檢視方塊便會出現在 [檢視方塊名稱] 資料行中，並顯示預設名稱 [檢視方塊]，如下圖所示。 請注意，每一個物件的核取方塊都會選取；除非您特別清除某個物件的核取方塊，否則這個檢視方塊與這個 Cube 的預設檢視方塊完全一樣。  
  
     ![檢視方塊名稱資料行中的新檢視方塊](../../2014/tutorials/media/l9-perspectives-2.gif "檢視方塊名稱資料行中的新檢視方塊")  
  
3.  將檢視方塊名稱變更為`Internet Sales`。  
  
4.  在下一個資料列上，將 [DefaultMeasure] 設定為 [網際網路銷售 - 銷售量]。  
  
     當使用者利用這個檢視方塊來瀏覽 Cube 時，這就是使用者會看到的量值 (除非他們另外指定其他量值)。  
  
    > [!NOTE]  
    >  您也可以在 Cube 的 [Cube 結構] 索引標籤之 [屬性] 視窗中，為整個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 設定預設量值。  
  
5.  清除下列物件的核取方塊：  
  
    -   `Reseller Sales` 量值群組  
  
    -   [銷售配額] 量值群組  
  
    -   [銷售配額 1] 量值群組  
  
    -   [轉售商] Cube 維度  
  
    -   [轉售商地理位置] Cube 維度  
  
    -   [銷售領域] Cube 維度  
  
    -   [員工] Cube 維度  
  
    -   [促銷] Cube 維度  
  
    -   [轉售商收入] KPI  
  
    -   [大型轉售商] 命名集  
  
    -   [總銷售量] 導出成員  
  
    -   [總產品成本] 導出成員  
  
    -   [轉售商毛利率] 導出成員  
  
    -   [總毛利率] 導出成員  
  
    -   [轉售商銷售與所有產品的比率] 導出成員  
  
    -   [總銷售與所有產品的比率] 導出成員  
  
     這些物件與網際網路銷售無關。  
  
    > [!NOTE]  
    >  您也可以在每個維度中，個別選取您要顯示在檢視方塊中的使用者定義階層和屬性。  
  
## <a name="defining-a-reseller-sales-perspective"></a>定義轉售商銷售檢視方塊  
  
1.  在 [檢視方塊] 索引標籤的工具列上，按一下 [新增檢視方塊] 按鈕。  
  
2.  變更至新的檢視方塊名稱`Reseller Sales`。  
  
3.  將 [轉售商銷售 - 銷售量] 設為預設量值。  
  
     當使用者利用這個檢視方塊來瀏覽 Cube 時，這個量值就是使用者會看到的量值 (除非他們另外指定其他量值)。  
  
4.  清除下列物件的核取方塊：  
  
    -   `Internet Sales` 量值群組  
  
    -   [網際網路銷售原因] 量值群組  
  
    -   [客戶] Cube 維度  
  
    -   [網際網路銷售訂單的詳細資料] Cube 維度  
  
    -   [銷售原因] Cube 維度  
  
    -   [網際網路銷售詳細資訊鑽研動作] 鑽研動作  
  
    -   [總銷售量] 導出成員  
  
    -   [總產品成本] 導出成員  
  
    -   [網際網路毛利率] 導出成員  
  
    -   [總毛利率] 導出成員  
  
    -   [網際網路銷售與所有產品的比率] 導出成員  
  
    -   [總銷售與所有產品的比率] 導出成員  
  
     這些物件與轉售商銷售無關。  
  
## <a name="defining-a-sales-summary-perspective"></a>定義銷售摘要檢視方塊  
  
1.  在 [檢視方塊] 索引標籤的工具列上，按一下 [新增檢視方塊] 按鈕。  
  
2.  變更至新的檢視方塊名稱`Sales Summary`。  
  
    > [!NOTE]  
    >  您不可以將導出量值指定為預設量值。  
  
3.  清除下列物件的核取方塊：  
  
    -   `Internet Sales` 量值群組  
  
    -   `Reseller Sales` 量值群組  
  
    -   [網際網路銷售原因] 量值群組  
  
    -   [銷售配額] 量值群組  
  
    -   [銷售配額1] 量值群組  
  
    -   [網際網路銷售訂單的詳細資料] Cube 維度  
  
    -   [銷售原因] Cube 維度  
  
    -   [網際網路銷售詳細資訊鑽研動作] 鑽研動作  
  
4.  選取下列物件的核取方塊：  
  
    -   [網際網路銷售計數] 量值  
  
    -   [轉售商銷售計數] 量值  
  
## <a name="browsing-the-cube-through-each-perspective"></a>透過每一個檢視方塊來瀏覽  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，請切換至 [瀏覽器] 索引標籤，然後按一下 [重新連接] 按鈕。  
  
3.  啟動 Excel。  
  
4.  [在 Excel 中進行分析] 會提示您選擇在 Excel 中瀏覽模型時要使用的檢視方塊，如下圖所示。  
  
     ![針對 網際網路銷售檢視方塊物件](../../2014/tutorials/media/l9-perspectives-3.gif "網際網路銷售檢視方塊物件")  
  
5.  或者，您可以從 Windows 的 [開始] 功能表啟動 Excel、在 localhost 上定義與 Analysis Services Tutorial 資料庫的連接，然後在 [資料連接] 精靈中選擇檢視方塊，如下圖所示。  
  
     ![在 Excel 中的資料連線精靈](../../2014/tutorials/media/l9-perspectives-3b.gif "在 Excel 中的資料連線精靈")  
  
6.  選取 `Internet Sales`中**觀點來看**清單，然後檢閱 [中繼資料] 窗格中的維度與量值。  
  
     請注意，只有那些針對 [網際網路銷售] 檢視方塊所指定的物件才會顯示出來。  
  
7.  在 [中繼資料] 窗格中，展開 [量值]。  
  
     請注意，只有`Internet Sales`量值群組隨即出現，一起**網際網路毛利率**並**網際網路銷售與所有產品的比率**導出成員。  
  
8.  在模型中，再次選取 Excel。 選取 [ `Sales Summary`]。  
  
     請注意，每一個量值群組只會出現一個量值，如下圖所示。  
  
     ![網際網路銷售 和 轉售商銷售的量值](../../2014/tutorials/media/l9-perspectives-4.gif "網際網路銷售 和 轉售商銷售的量值")  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [定義和瀏覽翻譯](../analysis-services/lesson-9-2-defining-and-browsing-translations.md)  
  
## <a name="see-also"></a>另請參閱  
 [檢視方塊](multidimensional-models-olap-logical-cube-objects/perspectives.md)   
 [多維度模型中的檢視方塊](multidimensional-models/perspectives-in-multidimensional-models.md)  
  
  
