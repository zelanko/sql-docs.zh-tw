---
title: 購物籃 DMX 教學課程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- market basket analysis [Analysis Services]
- tutorials [Data Mining]
- tutorials [DMX]
ms.assetid: 6e262a1d-c89e-4033-8368-46cf25168ef5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe12f1c4ca1c0946572c61e89f4f4edb8ba9a762
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185647"
---
# <a name="market-basket-dmx-tutorial"></a>購物籃 DMX 教學課程
  您將在此教學課程中學會如何使用資料採礦延伸模組 (DMX) 查詢語言，來建立、定型和探索採礦模型。 您將使用這些採礦模型來建立預測，說明哪些產品有可能同時被購買。  
  
 這些採礦模型將從 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 範例資料庫中包含的資料來建立，該資料庫儲存了虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的資料。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司。 該公司製造金屬類及複合型自行車，並銷售到北美、歐洲及亞洲的商業市場。 公司的基地位於美國華盛頓州的 Bothell 市，有 290 位員工，另外還有數個區域銷售團隊，分別位於國際銷售市場所在地。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 已決定要建立自訂應用程式，運用資料採礦功能來預測其客戶可能同時購買的產品類型。 自訂應用程式的目標是要能夠指定一組產品，並預測將與指定的產品一起購買的其他產品有哪些。 然後，[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 將使用此資訊將「建議」功能加入其網站中，並為呈現給其客戶的資訊提供更佳的組織方法。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供數個工具，可用來完成這項工作：  
  
-   DMX 查詢語言  
  
-   [Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查詢編輯器  
  
 資料採礦延伸模組 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一種查詢語言，您可以使用它來建立及處理採礦模型。 [!INCLUDE[msCoName](../includes/msconame-md.md)]關聯分析演算法建立模型來預測可能一起購買的產品。  
  
 此教學課程的目標是要提供將用於自訂應用程式的 DMX 查詢。  
  
 **如需詳細資訊：＜＞**[資料採礦方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>採礦結構和採礦模型  
 開始建立 DMX 陳述式之前，一定要先了解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來建立採礦模型的主要物件。 *採礦結構*是定義從中建立採礦模型的資料網域的資料結構。 單一採礦結構可以包含多個*採礦模型*，共用相同的網域。 採礦模型會將採礦模型演算法套用至以採礦結構表示的資料。  
  
 採礦結構的建置組塊是採礦結構資料行，它們會描述資料來源包含的資料。 這些資料行包含如資料類型、內容類型和資料散發方式等資訊。  
  
 採礦模型必須包含採礦結構所描述的索引鍵資料行，以及剩餘資料行的子集。 採礦模型定義每一個資料行的使用方式，以及定義用來建立採礦模型的演算法。 例如，在 DMX 中，您可以指定資料行為索引鍵資料行或 PREDICT 資料行。 如果未指定資料行，則假設它是輸入資料行。  
  
 在 DMX 中，有兩種方式建立採礦模型。 您可以使用 `CREATE MINING MODEL` 陳述式來同時建立採礦結構和相關聯的採礦模型，也可以先使用 `CREATE MINING STRUCTURE` 陳述式來建立採礦結構，然後使用 `ALTER STRUCTURE` 陳述式，將採礦模型加入至結構。 以下將描述這些方法。  
  
 `CREATE MINING MODEL`  
 使用此陳述式可同時建立使用相同名稱的採礦結構和相關聯的採礦模型。 採礦模型名稱後面會加上 "Structure"，以便與採礦結構區別。  
  
 如果您要建立包含單一採礦模型的採礦結構，則此陳述式很有幫助。  
  
 如需詳細資訊，請參閱 [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)。  
  
 CREATE MINING STRUCTURE  
 使用這個陳述式可建立新的採礦結構而不使用任何模型。  
  
 當您使用 CREATE MINING STRUCTURE 時，您也可以建立鑑效組資料集，該資料集可用來測試以相同採礦結構為根據的任何模型。  
  
 如需詳細資訊，請參閱 [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)。  
  
 `ALTER MINING STRUCTURE`  
 使用此陳述式將採礦模型加入已存在於伺服器上的採礦結構中。  
  
 您要在單一採礦結構中加入不止一個採礦模型，有幾個原因。 例如，您可以使用不同演算法來建立數個採礦模型，看看哪一個最好用。 或者，您也可以建立數個使用相同演算法的採礦模型，但每一個採礦模型要設定不同的參數，以找出該參數的最佳設定。  
  
 如需詳細資訊，請參閱 < [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)。  
  
 因為您要建立包含數個採礦模型的採礦結構，所以您將使用此教學課程的第二個方法。  
  
 **如需詳細資訊**  
  
 [資料採礦延伸模組&#40;DMX&#41;參考](/sql/dmx/data-mining-extensions-dmx-reference)，[了解 DMX Select 陳述式](/sql/dmx/understanding-the-dmx-select-statement)，[結構和使用方式的 DMX 預測查詢](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程分成下列課程：  
  
 [第 1 課：建立購物籃採礦結構](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md)  
 在這一課，您將學會如何使用 `CREATE` 陳述式來建立採礦結構。  
  
 [第 2 課：將採礦模型加入購物籃採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
 在這一課，您將學會如何使用 `ALTER` 陳述式將採礦模型加入至採礦結構。  
  
 [第 3 課：處理購物籃採礦結構](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
 在這一課，您將學會如何使用 `INSERT INTO` 陳述式來處理採礦結構及其相關聯的採礦模型。  
  
 [第 4 課：執行購物籃預測](../../2014/tutorials/lesson-4-executing-market-basket-predictions.md)  
 在這一課，您將學會如何使用 `PREDICTION JOIN` 陳述式來建立採礦模型的預測。  
  
## <a name="requirements"></a>需求  
 在執行此教學課程之前，請確定有安裝下列各項：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫  
  
 為了加強安全性，系統預設不會安裝範例資料庫。 若要安裝的正式範例資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請前往[ http://www.CodePlex.com/MSFTDBProdSamples ](https://go.microsoft.com/fwlink/?LinkId=88417)或在 Microsoft SQL Server Samples and Community Projects 首頁上，在 [Microsoft SQL Server Product Samples] 區段。 按一下 **資料庫**，然後按一下**版本**索引標籤，然後選取您想要的資料庫。  
  
> [!NOTE]  
>  當檢閱教學課程時，我們建議您將新增**下一個主題**並**上一個主題**文件檢視器工具列的按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [Bike Buyer DMX 教學課程](../../2014/tutorials/bike-buyer-dmx-tutorial.md)   
 [資料採礦基本教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [第 3 課：建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
  
