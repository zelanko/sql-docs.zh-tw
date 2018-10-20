---
title: Bike Buyer DMX 教學課程 |Microsoft Docs
ms.custom: ''
ms.date: 10/19/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- DMX [Analysis Services], tutorials
- data mining [Analysis Services], tutorials
- statements [DMX], tutorials
- Data Mining Extensions [Analysis Services], tutorials
- tutorials [Data Mining]
ms.assetid: 4b634cc1-86dc-42ec-9804-a19292fe8448
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25ca6a8a5769da023da506c25c858a012b7f7a7c
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49462014"
---
# <a name="bike-buyer-dmx-tutorial"></a>Bike Buyer DMX 教學課程
  您將在此教學課程中學會如何使用資料採礦延伸模組 (DMX) 查詢語言，來建立、培訓和探索採礦模型。 您將使用這些採礦模型來建立預測，以判斷客戶是否要購買自行車。  
  
 這些採礦模型將從 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 範例資料庫中包含的資料來建立，該資料庫儲存了虛構公司 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的資料。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨國製造公司。 該公司製造金屬類及複合型自行車，並銷售到北美、歐洲及亞洲的商業市場。 公司的基地位於美國華盛頓州的 Bothell 市，有 290 位員工，另外還有數個區域銷售團隊，分別位於國際銷售市場所在地。  
  
## <a name="tutorial-scenario"></a>教學課程案例  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 決定要建立自訂應用程式，使用資料採礦功能來擴大其資料分析。 自訂應用程式的目標是要能夠：  
  
-   以潛在客戶的特性做為輸入，並預測他們是否會購買自行車。  
  
-   以潛在客戶清單及客戶特性做為輸入，並預測誰會購買自行車。  
  
 在第一個案例中，客戶資料是由客戶註冊頁提供，在第二個案例中，潛在客戶的清單是由 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 行銷部門提供。  
  
 此外，行銷部門要求能夠將現有客戶依特性分類，例如居住地、子女人數及通勤距離。 他們想知道是否能使用群集來幫助鎖定特定客戶群。 這需要其他採礦模型。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供數個工具，可用來完成這些工作：  
  
-   DMX 查詢語言  
  
-   [Microsoft 決策樹演算法](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)而[Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的查詢編輯器  
  
 資料採礦延伸模組 (DMX) 是 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的一種查詢語言，您可以使用它來建立及處理採礦模型。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法建立可用來預測某人是否會購買自行車的模型。 產生的模型可以用個別使用者或客戶資料表做為輸入。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 群集演算法可依共用特性建立客戶群組。 此教學課程的目標是要提供用於自訂應用程式的 DMX 指令碼。  
  
 **如需詳細資訊：** [資料採礦方案](../../2014/analysis-services/data-mining/data-mining-solutions.md)  
  
## <a name="mining-structure-and-mining-models"></a>採礦結構和採礦模型  
 開始建立 DMX 陳述式之前，一定要先了解 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用來建立採礦模型的主要物件。 資料採礦結構是定義資料網域 (從中建立採礦模型) 的資料結構。 單一採礦結構可包含共用相同網域的多個採礦模型。 採礦模型會將採礦模型演算法套用至以採礦結構表示的資料。  
  
 採礦結構的建置組塊是採礦結構資料行，它們會描述資料來源包含的資料。 這些資料行包含如資料類型、內容類型和資料散發方式等資訊。  
  
 採礦模型必須包含採礦結構所描述的索引鍵資料行，以及剩餘資料行的子集。 採礦模型定義每一個資料行的使用方式，以及定義用來建立採礦模型的演算法。 例如，在 DMX 中，您可以指定資料行為索引鍵資料行或 PREDICT 資料行。 如果未指定資料行，則假設它是輸入資料行。  
  
 在 DMX 中，有兩種方式建立採礦模型。 您可以使用 CREATE MINING MODEL 陳述式，同時建立採礦結構和相關聯的採礦模型，也可以先使用 CREATE MINING STRUCTURE 陳述式建立採礦結構，然後使用 ALTER STRUCTURE 陳述式將採礦模型加入結構中。 下表將描述這些方法。  
  
 CREATE MINING MODEL  
 使用此陳述式可同時建立使用相同名稱的採礦結構和相關聯的採礦模型。 採礦模型名稱後面會加上 "Structure"，以便與採礦結構區別。 如果您要建立包含單一採礦模型的採礦結構，則此陳述式很有幫助。  
  
 如需詳細資訊，請參閱 [CREATE MINING MODEL &#40;DMX&#41;](/sql/dmx/create-mining-model-dmx)。  
  
 ALTER MINING STRUCTURE  
 使用此陳述式將採礦模型加入已存在於伺服器上的採礦結構中。 如果您想要建立包含數個不同採礦模型的採礦結構，則此陳述式很有幫助。 您要在單一採礦結構中加入不止一個採礦模型，有幾個原因。 例如，您可以建立數個使用不同演算法的採礦模型，看看哪一個最好用。 您可以建立數個使用相同演算法的採礦模型，但每一個採礦模型要設定不同的參數，以找出參數的最佳設定。  
  
 如需詳細資訊，請參閱 < [ALTER MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/alter-mining-structure-dmx?view=sql-server-2016)。  
  
 因為您要建立包含數個採礦模型的採礦結構，所以您將使用此教學課程的第二個方法。  
  
 **如需詳細資訊**  
  
 [資料採礦延伸模組&#40;DMX&#41;參考](/sql/dmx/data-mining-extensions-dmx-reference)，[了解 DMX Select 陳述式](/sql/dmx/understanding-the-dmx-select-statement)，[結構和使用方式的 DMX 預測查詢](/sql/dmx/structure-and-usage-of-dmx-prediction-queries)  
  
## <a name="what-you-will-learn"></a>學習內容  
 這個教學課程分成下列課程：  
  
 [第 1 課：建立自行車買主採礦結構](../../2014/tutorials/lesson-1-creating-the-bike-buyer-mining-structure.md)  
 在這一課，您將學會如何使用 `CREATE` 陳述式來建立採礦結構。  
  
 [第 2 課：將採礦模型新增至自行車買主採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
 在這一課，您將學會如何使用 `ALTER` 陳述式將採礦模型加入至採礦結構。  
  
 [第 3 課：處理自行車買主採礦結構](../../2014/tutorials/lesson-3-processing-the-bike-buyer-mining-structure.md)  
 在這一課，您將學會如何使用 `INSERT INTO` 陳述式來處理採礦結構及其相關聯的採礦模型。  
  
 [第 4 課：瀏覽自行車買主採礦模型](../../2014/tutorials/lesson-4-browsing-the-bike-buyer-mining-models.md)  
 在這一課，您將學會如何使用 `SELECT` 陳述式來探索採礦模型的內容。  
  
 [第 5 課：執行預測查詢](../../2014/tutorials/lesson-5-executing-prediction-queries.md)  
 在這一課，您將學會如何使用 `PREDICTION JOIN` 陳述式來建立採礦模型的預測。  
  
## <a name="requirements"></a>需求  
 在執行此教學課程之前，請確定有安裝下列各項：  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)][!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]， [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]，或 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] 資料庫。 為了加強安全性，系統預設不會安裝範例資料庫。 若要安裝的正式範例資料庫[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請瀏覽[Microsoft SQL Sample Databases](http://go.microsoft.com/fwlink/?LinkId=88417)頁面，然後選取您想要安裝的資料庫...  
  
> [!NOTE]  
>  當檢閱教學課程時，我們建議您將新增**下一個主題**並**上一個主題**文件檢視器工具列的按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [購物籃 DMX 教學課程](../../2014/tutorials/market-basket-dmx-tutorial.md)   
 [基本資料採礦教學課程](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
  
