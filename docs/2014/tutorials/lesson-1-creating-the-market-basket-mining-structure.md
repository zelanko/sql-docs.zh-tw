---
title: 第1課：建立購物籃的採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a817c8d1-aff4-42b4-b194-ad9cc1c60f35
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6a6e123e525512a72d70bcc8ca2eba549d1347e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62676261"
---
# <a name="lesson-1-creating-the-market-basket-mining-structure"></a>第 1 課：建立購物籃採礦結構
  在這一課，您將建立一個可讓您預測客戶可能同時購買哪些 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 產品的採礦結構。 如果您不熟悉在資料採礦中使用的是採礦結構和其角色，請參閱[&#40;Analysis Services 資料採礦&#41;的採礦結構](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 您在本課程中建立的關聯性採礦結構，支援加入以[Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)為基礎的採礦模型。 在後面的課程中，您將使用採礦模型來預測客戶可能同時購買的產品類型，這稱為購物籃分析。 例如，您會發現客戶可能同時購買越野車、輪胎和頭盔。  
  
 在這一課，採礦結構是使用巢狀資料表來定義。 使用巢狀資料表是因為結構所要定義的資料網域是包含在兩個不同的來源資料表中。 如需有關嵌套資料表的詳細資訊，請參閱[Analysis Services 資料採礦&#41;的嵌套資料表 &#40;](../../2014/analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)。  
  
## <a name="create-mining-structure-statement"></a>CREATE MINING STRUCTURE 陳述式  
 若要建立包含嵌套資料表的「採礦結構」，您可以使用「[建立」採礦結構 &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx)語句。 陳述式中的程式碼可分成下列各部份：  
  
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
  
 如需在 DMX 中命名物件的詳細資訊，請參閱[dmx&#41;&#40;的識別碼](/sql/dmx/identifiers-dmx)。  
  
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
  
 如需您可以定義的「採礦結構」資料行類型的詳細資訊，請參閱「[採礦結構資料行](../../2014/analysis-services/data-mining/mining-structure-columns.md)」。  
  
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
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 [**連接到伺服器**] 對話方塊的 [**伺服器類型**] 中，選取 [ **Analysis Services**]。 在 [**伺服器名稱**] `LocalHost`中，輸入，或您想要[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]在本課程中連接之實例的名稱。 按一下 [ **連接**]。  
  
3.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
## <a name="altering-the-query"></a>改變查詢  
 下一步是修改上述 CREATE MINING STRUCTURE 陳述式來建立購物籃採礦結構。  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>若要自訂 CREATE MINING STRUCTURE 陳述式  
  
1.  在查詢編輯器中，將 CREATE MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
2.  取代下列項目：  
  
    ```  
    [mining structure name]   
    ```  
  
     取代為  
  
    ```  
    [Market Basket]  
    ```  
  
3.  取代下列項目：  
  
    ```  
    <key column>  
    ```  
  
     取代為  
  
    ```  
    OrderNumber TEXT KEY  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <table columns>  
    (  <nested key column>,  
       <nested mining structure columns> )  
    ```  
  
     取代為  
  
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
  
5.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
6.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`Market Basket Structure.dmx`將檔案命名為。  
  
## <a name="executing-the-query"></a>執行查詢  
 最後的步驟是執行查詢。 在建立及儲存查詢之後，需要執行它 (也就是需要執行陳述式) 才能在伺服器上建立採礦結構。 如需在 [查詢編輯器] 中執行查詢的詳細資訊，請參閱[資料庫引擎查詢編輯器 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>若要執行查詢  
  
-   在 [查詢編輯器] 的工具列上，按一下 [**執行**]。  
  
     查詢的狀態會在語句完成執行之後，顯示在 [查詢編輯器] 底部的 [**訊息**] 索引標籤中。 訊息應該顯示如下：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     伺服器上現在有一個名為「**購物籃**」的新結構。  
  
 在下一課，您會將採礦模型加入剛才建立的購物籃採礦結構中。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：將採礦模型加入購物籃採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-market-basket-mining-structure.md)  
  
  
