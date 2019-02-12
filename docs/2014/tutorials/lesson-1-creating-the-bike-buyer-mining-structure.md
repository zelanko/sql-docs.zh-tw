---
title: 第 1 課：建立自行車買主採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a73ac60b-660f-458a-bd2f-993fbeba7226
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d6384910858d87a80aa3c8f897bc88e45f4504fb
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025799"
---
# <a name="lesson-1-creating-the-bike-buyer-mining-structure"></a>第 1 課：建立自行車買主採礦結構
  在這一課，您將建立一個可讓您預測 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 的潛在客戶是否將購買自行車的採礦結構。 如果您不熟悉採礦結構和資料採礦中的其角色，請參閱[採礦結構&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)。  
  
 在這一課，您將建立的 Bike Buyer 採礦結構支援加入為基礎的採礦模型[Microsoft 群集演算法](../../2014/analysis-services/data-mining/microsoft-clustering-algorithm.md)[Microsoft Decision Trees Algorithm](../../2014/analysis-services/data-mining/microsoft-decision-trees-algorithm.md)。 在後面的課程中，您將使用群集採礦模型來探索可分組客戶的不同方式，並將使用決策樹採礦模型來預測潛在客戶是否會購買自行車。  
  
## <a name="create-mining-structure-statement"></a>CREATE MINING STRUCTURE 陳述式  
 若要建立採礦結構時，您使用[CREATE MINING STRUCTURE &#40;DMX&#41; ](/sql/dmx/create-mining-structure-dmx)陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   命名結構。  
  
-   定義索引鍵資料行。  
  
-   定義採礦資料行。  
  
-   定義選擇性的測試資料集。  
  
 以下是 CREATE MINING STRUCTURE 陳述式的一般範例：  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
(  
    <key column>,  
    <mining structure columns>  
)   
WITH HOLDOUT (<holdout specifier>)  
```  
  
 程式碼的第一行定義結構的名稱：  
  
```  
CREATE MINING STRUCTURE [<mining structure name>]  
```  
  
 如需命名物件中的資料採礦延伸模組 (DMX) 的資訊，請參閱[識別碼&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 程式碼的下一行定義採礦結構的索引鍵資料行，可唯一識別來源資料中的實體：  
  
```  
<key column>,  
```  
  
 在您要建立的採礦結構中，客戶識別碼 `CustomerKey` 定義來源資料中的實體。  
  
 程式碼的下一行用來定義採礦資料行，與採礦結構相關聯的採礦模型將使用這些資料行：  
  
```  
<mining structure columns>  
```  
  
 您可以使用 DISCRETIZE 函數內\<採礦結構資料行 > 離散化連續資料行，使用下列語法：  
  
 `DISCRETIZE(<method>,<number of buckets>)`  
  
 如需有關分隔資料行的詳細資訊，請參閱 <<c0> [ 離散化方法&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md)。</c0> 如需詳細的採礦結構資料行，您可以定義類型的詳細資訊，請參閱[採礦結構資料行](../../2014/analysis-services/data-mining/mining-structure-columns.md)。  
  
 程式碼的最後一行定義採礦結構中的選擇性資料分割：  
  
```  
WITH HOLDOUT (<holdout specifier>)  
```  
  
 您將資料的某些部分指定為用來測試與結構相關的採購模型，而將剩餘的資料指定為用來定型模型。 根據預設，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 所建立的測試資料集會包含所有案例資料的 30%。 您要加入規格，規定測試資料集應該包含 30% 的案例，最多可達 1000 個案例。 如果 30% 的案例數少於 1000，則測試資料集將包含較小的數量。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   建立新的空白查詢。  
  
-   改變查詢來建立採礦結構。  
  
-   執行查詢。  
  
## <a name="creating-the-query"></a>建立查詢  
 第一步是連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體，並在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中建立新的 DMX 查詢。  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中建立新的 DMX 查詢  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 [**連接到伺服器**] 對話方塊中，如**伺服器類型**，選取**Analysis Services**。 在**伺服器名稱**，型別`LocalHost`，輸入執行個體的名稱或[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您想要連接到這一課。 按一下 **[連接]**。  
  
3.  中**物件總管 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下**DMX**以開啟**查詢編輯器**以及新的空白查詢。  
  
## <a name="altering-the-query"></a>改變查詢  
 下一步是修改上述 CREATE MINING STRUCTURE 陳述式來建立自行車買主採礦結構。  
  
#### <a name="to-customize-the-create-mining-structure-statement"></a>若要自訂 CREATE MINING STRUCTURE 陳述式  
  
1.  在查詢編輯器中，將 CREATE MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
2.  取代下列項目：  
  
    ```  
    [<mining structure>]   
    ```  
  
     成為：  
  
    ```  
    [Bike Buyer]  
    ```  
  
3.  取代下列項目：  
  
    ```  
    <key column>   
    ```  
  
     成為：  
  
    ```  
    CustomerKey LONG KEY  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining structure columns>   
    ```  
  
     成為：  
  
    ```  
    [Age] LONG DISCRETIZED(Automatic,10),  
    [Bike Buyer] LONG DISCRETE,  
    [Commute Distance] TEXT DISCRETE,  
    [Education] TEXT DISCRETE,  
    [Gender] TEXT DISCRETE,  
    [House Owner Flag] TEXT DISCRETE,  
    [Marital Status] TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Number Children At Home] LONG DISCRETE,  
    [Occupation] TEXT DISCRETE,  
    [Region] TEXT DISCRETE,  
    [Total Children]LONG DISCRETE,  
    [Yearly Income] DOUBLE CONTINUOUS  
    ```  
  
5.  取代下列項目：  
  
    ```  
    WITH HOLDOUT (holdout specifier>)  
    ```  
  
     成為：  
  
    ```  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
    ```  
  
     現在，完整的採礦結構陳述式應該如下所示：  
  
    ```  
    CREATE MINING STRUCTURE [Bike Buyer]  
    (  
       [Customer Key] LONG KEY,  
       [Age]LONG DISCRETIZED(Automatic,10),  
       [Bike Buyer] LONG DISCRETE,  
       [Commute Distance] TEXT DISCRETE,  
       [Education] TEXT DISCRETE,  
       [Gender] TEXT DISCRETE,  
       [House Owner Flag] TEXT DISCRETE,  
       [Marital Status] TEXT DISCRETE,  
       [Number Cars Owned]LONG DISCRETE,  
       [Number Children At Home]LONG DISCRETE,  
       [Occupation] TEXT DISCRETE,  
       [Region] TEXT DISCRETE,  
       [Total Children]LONG DISCRETE,  
       [Yearly Income] DOUBLE CONTINUOUS  
    )  
    WITH HOLDOUT (30 PERCENT or 1000 CASES)  
  
    ```  
  
6.  在 **檔案**功能表上，按一下**另存 DMXQuery1.dmx 為**。  
  
7.  在 [**另存新檔**] 對話方塊中，瀏覽至適當的資料夾，並將檔案命名`Bike Buyer Structure.dmx`。  
  
## <a name="executing-the-query"></a>執行查詢  
 最後的步驟是執行查詢。 在建立及儲存查詢以後，將需要執行查詢。 也就是說，必須執行此陳述式，才能夠在伺服器上建立採礦結構。 如需有關如何在 [查詢編輯器] 中執行查詢的詳細資訊，請參閱 < [Database Engine 查詢編輯器&#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>若要執行查詢  
  
1.  在查詢編輯器的工具列上，按一下**Execute**。  
  
     查詢的狀態會顯示在**訊息**編輯器 底部的查詢陳述式完成執行之後的索引標籤。 訊息應該顯示如下：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     新的結構，名為**Bike Buyer**現在存在於伺服器上。  
  
 在下一課，您會將採礦模型加入剛才建立的結構中。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：將採礦模型加入 Bike Buyer 採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-bike-buyer-mining-structure.md)  
  
  
