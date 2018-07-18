---
title: 第 1 課： 建立購物籃採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a817c8d1-aff4-42b4-b194-ad9cc1c60f35
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f719a4dd11234a361856dcf170eebcd3856f66c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323608"
---
# <a name="lesson-1-creating-the-market-basket-mining-structure"></a>第 1 課：建立購物籃採礦結構
  在這一課，您將建立一個可讓您預測客戶可能同時購買哪些 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 產品的採礦結構。 如果您不熟悉採礦結構和資料採礦中的其角色，請參閱[採礦結構&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 在這一課，您將建立的關聯採礦結構支援加入採礦模型，根據[Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)。 在後面的課程中，您將使用採礦模型來預測客戶可能同時購買的產品類型，這稱為購物籃分析。 例如，您會發現客戶可能同時購買越野車、輪胎和頭盔。  
  
 在這一課，採礦結構是使用巢狀資料表來定義。 使用巢狀資料表是因為結構所要定義的資料網域是包含在兩個不同的來源資料表中。 如需有關巢狀資料表的詳細資訊，請參閱[巢狀資料表&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
## <a name="create-mining-structure-statement"></a>CREATE MINING STRUCTURE 陳述式  
 若要建立採礦結構包含巢狀的資料表，您使用[CREATE MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/create-mining-structure-dmx)陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   命名結構  
  
-   定義索引鍵資料行  
  
-   定義採礦資料行  
  
-   定義巢狀資料表資料行  
  
 以下是 CREATE MINING STRUCTURE 陳述式的一般範例：  
  
```  
CREATE MINING STRUCTURE [<Mining Structure Name>]  
(  
   <key column>,  
   <mining structure columns>,  
   <table columns>  
   (  <nested key column>,  
      <nested mining structure columns> )  
)  
  
```  
  
 程式碼的第一行定義結構的名稱：  
  
```  
CREATE MINING STRUCTURE [Mining Structure Name]  
```  
  
 如需命名的物件，在 DMX 中的資訊，請參閱[識別碼&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 程式碼的下一行定義採礦結構的索引鍵資料行，可唯一識別來源資料中的實體：  
  
```  
<key column>  
```  
  
 程式碼的下一行用來定義採礦資料行，與採礦結構相關聯的採礦模型將使用這些資料行：  
  
```  
<mining structure columns>  
```  
  
 接下來的幾行程式碼會定義巢狀資料表資料行：  
  
```  
<table columns>  
(  <nested key column>,  
   <nested mining structure columns> )  
```  
  
 如需採礦結構資料行，您可以定義類型的資訊，請參閱[採礦結構資料行](../../2014/analysis-services/data-mining/mining-structure-columns.md)。  
  
> [!NOTE]  
>  根據預設，[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 會針對每個採礦結構建立百分之 30 的鑑效組資料集；但是，當您使用 DMX 來建立採礦結構時，您必須在需要時手動加入鑑效組資料集。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   建立新的空白查詢  
  
-   改變查詢來建立採礦結構  
  
-   執行查詢  
  
## <a name="creating-the-query"></a>建立查詢  
 第一步是連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體，並在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中建立新的 DMX 查詢。  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中建立新的 DMX 查詢  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
2.  在 [**連接到伺服器**] 對話方塊中，如**伺服器類型**，選取**Analysis Services**。 在 **伺服器名稱**，型別`LocalHost`，或執行個體名稱[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要連接到這一課。 按一下 **[連接]**。  
  
3.  中**物件總管**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
## <a name="altering-the-query"></a>改變查詢  
 下一步是修改上述 CREATE MINING STRUCTURE 陳述式來建立購物籃採礦結構。  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>若要自訂 CREATE MINING STRUCTURE 陳述式  
  
1.  在查詢編輯器中，將 CREATE MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
2.  取代下列項目：  
  
    ```  
    [mining structure name]   
    ```  
  
     成為：  
  
    ```  
    [Market Basket]  
    ```  
  
3.  取代下列項目：  
  
    ```  
    <key column>  
    ```  
  
     成為：  
  
    ```  
    OrderNumber TEXT KEY  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <table columns>  
    (  <nested key column>,  
       <nested mining structure columns> )  
    ```  
  
     成為：  
  
    ```  
    [Products] TABLE (  
        [Model] TEXT KEY  
    )  
    ```  
  
     TEXT KEY 語言指定 [模型] 資料行是巢狀資料表的索引鍵資料行。  
  
     現在，完整的採礦結構陳述式應該如下所示：  
  
    ```  
    CREATE MINING STRUCTURE [Market Basket] (  
        OrderNumber TEXT KEY,  
        [Products] TABLE (  
            [Model] TEXT KEY  
        )  
    )  
    ```  
  
5.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
6.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Market Basket Structure.dmx`。  
  
## <a name="executing-the-query"></a>執行查詢  
 最後的步驟是執行查詢。 在建立及儲存查詢之後，需要執行它 (也就是需要執行陳述式) 才能在伺服器上建立採礦結構。 如需有關如何在 [查詢編輯器] 中執行查詢的詳細資訊，請參閱 < [Database Engine 查詢編輯器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>若要執行查詢  
  
-   在查詢編輯器的工具列上，按一下**Execute**。  
  
     查詢的狀態會顯示在**訊息**編輯器 底部的查詢陳述式完成執行之後的索引標籤。 訊息應該顯示如下：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     新的結構，名為**購物籃**現在存在於伺服器上。  
  
 在下一課，您會將採礦模型加入剛才建立的購物籃採礦結構中。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：將採礦模型新增至購物籃採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
  
  
