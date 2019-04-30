---
title: 定義導出成員 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 07f13e1c-0b20-4f9e-ad62-c438983f2785
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0d9411ab88d259718aaa62873e615a62efdd82e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728926"
---
# <a name="defining-calculated-members"></a>定義導出成員
  導出成員是根據 Cube 資料、算術運算子、數字和函數組合所定義的維度成員或量值群組成員。 例如，您可以建立一個導出成員，計算 Cube 中兩個實體量值的總和。 導出成員定義是儲存在 Cube 中，但其值是在查詢時計算。  
  
 若要建立導出成員，請在 Cube 設計師的 [計算] 索引標籤上使用 [新增導出成員] 命令。 您可以在任何維度 (包括量值維度) 內建立導出成員， 也可以在 [計算屬性] 對話方塊中的顯示資料夾內放置導出成員。 如需詳細資訊，請參閱[計算](multidimensional-models-olap-logical-cube-objects/calculations.md)、[多維度模型中的計算](multidimensional-models/calculations-in-multidimensional-models.md)和[建立導出成員](multidimensional-models/create-calculated-members.md)。  
  
 在本主題的工作中，您要定義導出成員，讓使用者檢視網際網路銷售、轉售商銷售和所有銷售的毛利率百分比和銷售比率。  
  
## <a name="defining-calculations-to-aggregate-physical-measures"></a>將計算定義為彙總實體量值  
  
1.  開啟適用於 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 的 Cube 設計師，然後按一下 [計算] 索引標籤。  
  
     請注意 [計算運算式] 窗格和 [指令碼組合管理] 窗格中的預設 CALCULATE 命令。 這個命令會指定 Cube 中的量值，根據其 AggregateFunction 屬性所指定的值加以彙總。 量值是以一般方式加總，不過也可以用其他方式計算或彙總。  
  
     下圖顯示 Cube 設計師的 [計算] 索引標籤。  
  
     ![計算索引標籤，Cube 設計師](../../2014/tutorials/media/l6-calculatedmembers-1.gif "計算索引標籤，Cube 設計師 的")  
  
2.  在 [計算] 索引標籤的工具列上，按一下 [新增導出成員]。  
  
     [計算運算式] 窗格即會出現新的表單，您可在該窗格中定義這個新導出成員的屬性。 新成員也會出現在 [指令碼組合管理] 窗格中。  
  
     下圖顯示當您按一下 [新增導出成員] 時，出現在 [計算運算式] 窗格的表單。  
  
     ![計算運算式窗格表單](../../2014/tutorials/media/l6-calculatedmembers-02.gif "計算運算式窗格表單")  
  
3.  在 **名稱**方塊中，變更導出量值名稱`[Total Sales Amount]`。  
  
     如果導出成員的名稱包含空格，則必須以方括號括住導出成員的名稱。  
  
     請注意，在 [父階層] 清單中，新的導出成員預設是以 [量值] 維度建立的。 量值維度中的導出成員，也常被稱為導出量值。  
  
4.  在 [計算] 索引標籤 [計算工具] 窗格中，展開 [中繼資料] 索引標籤上的 [量值]，再展開 [網際網路銷售] 以檢視 [網際網路銷售] 量值群組的中繼資料。  
  
     您可以將中繼資料元素，從 [計算工具] 窗格拖曳到 [運算式] 方塊中，再加上運算子和其他元素，來建立多維度運算式 (MDX) 運算式。 或者，您也可以在 [運算式] 方塊中，直接輸入 MDX 運算式。  
  
    > [!NOTE]  
    >  如果您無法在 [計算工具] 窗格中檢視任何中繼資料，請在工具列上按一下 [重新連接]。 如果此舉無效，可能得處理 Cube，或者啟動 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。  
  
5.  從 [計算工具] 窗格的 [中繼資料] 索引標籤，將 [網際網路銷售 - 銷售量] 拖曳到 [計算運算式] 窗格中的 [運算式] 方塊。  
  
6.  在 **運算式**方塊中，輸入一個加號 (`+`) 之後 **[Measures]。 [網際網路銷售-銷售量]**。  
  
7.  在 [計算工具] 窗格的 [中繼資料] 索引標籤中，展開 [轉售商銷售]，再將 [轉售商銷售 - 銷售量] 拖曳到 [計算運算式] 窗格中 [運算式] 方塊的加號 (+) 後面。  
  
8.  在 [格式字串] 清單中，選取 [貨幣]。  
  
9. 在 [非空白行為] 清單中，勾選 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
     您在 [非空白行為] 清單所指定的量值，是用於解析 MDX 的 NON EMPTY 查詢。 如果所有指定的量值都是空的，那麼當您在 [非空白行為] 清單中指定一或多個量值時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會把導出成員視為空白。 如果 [非空白行為] 屬性空白，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 必須評估導出成員本身，來判定該成員是否為空白。  
  
     下圖顯示 [計算運算式] 窗格，其中含有您在前面步驟所指定的設定。  
  
     ![Populated 計算運算式 窗格](../../2014/tutorials/media/l6-calculatedmembers-03.gif "填入計算運算式 窗格")  
  
10. 在 [計算] 索引標籤的工具列上，按一下 [指令碼檢視]，然後再檢閱 [計算運算式] 窗格中的計算指令碼。  
  
     請注意，新的計算值會加入初始的 CALCULATE 運算式中；每個個別計算值都以分號區隔。 同時也請注意，註解會出現在計算指令碼的開頭。 在計算群組的計算指令碼中加入註解，有助於您自己和其他開發人員了解複雜的計算指令碼。  
  
11. 在計算指令碼的 **Calculate;** 命令之後、剛新增的計算指令碼之前，新增一行，然後把下列文字新增到指令碼的那一行：  
  
    ```  
    /* Calculations to aggregate Internet Sales and Reseller Sales measures */  
    ```  
  
     下圖顯示此時在教學課程中應該顯示在 [計算運算式] 窗格的計算指令碼。  
  
     ![在 [計算運算式] 窗格中的指令碼](../../2014/tutorials/media/l6-calculatedmembers-04.gif "計算運算式窗格中的指令碼")  
  
12. 工具列上的**計算**索引標籤上，按一下**表單檢視**，確認`[Total Sales Amount]`中選取**指令碼組合管理**窗格中，然後再按一下**新的導出的成員**。  
  
13. 變更到這個新導出成員的名稱`[Total Product Cost]`，然後建立中的下列運算式**運算式**方塊：  
  
    ```  
    [Measures].[Internet Sales-Total Product Cost] + [Measures].[Reseller Sales-Total Product Cost]  
    ```  
  
14. 在 [格式字串] 清單中，選取 [貨幣]。  
  
15. 在 [非空白行為] 清單中，勾選 [網際網路銷售 - 總產品成本] 和 [轉售商銷售 - 總產品成本] 的核取方塊，然後按一下 [確定]。  
  
     現在您已經定義了兩個導出成員，兩個都會出現在 [指令碼組合管理] 窗格中。 這些導出成員可被您在計算指令碼後半段所定義的其他計算使用。 您可以在 [指令碼組合管理] 窗格中，選取任何導出成員，以檢視該導出成員的定義；該導出成員的定義會顯示在表單檢視的 [計算運算式] 窗格中。 但是新定義的導出成員在部署之前，不會顯示在 [計算工具] 窗格中。 計算並不需要處理。  
  
## <a name="defining-gross-profit-margin-calculations"></a>定義毛利率計算  
  
1.  確認`[Total Product Cost]`中選取**指令碼組合管理**窗格中，然後再按一下**新增導出成員**工具列上的**計算** 索引標籤。  
  
2.  在 **名稱**方塊中，變更到這個新導出量值名稱`[Internet GPM]`。  
  
3.  在 [運算式] 方塊中，建立下列 MDX 運算式：  
  
    ```  
    ([Measures].[Internet Sales-Sales Amount] -   
    [Measures].[Internet Sales-Total Product Cost]) /  
    [Measures].[Internet Sales-Sales Amount]  
    ```  
  
4.  在 [格式字串] 清單中，選取 [百分比]。  
  
5.  在 [非空白行為] 清單中，勾選 [網際網路銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
6.  在 [計算] 索引標籤的工具列上，按一下 [新增導出成員]。  
  
7.  在 **名稱**方塊中，變更到這個新導出量值名稱`[Reseller GPM]`。  
  
8.  在 [運算式] 方塊中，建立下列 MDX 運算式：  
  
    ```  
    ([Measures].[Reseller Sales-Sales Amount] -   
    [Measures].[Reseller Sales-Total Product Cost]) /  
    [Measures].[Reseller Sales-Sales Amount]  
    ```  
  
9. 在 [格式字串] 清單中，選取 [百分比]。  
  
10. 在 [非空白行為] 清單中，勾選 [轉售商銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
11. 在 [計算] 索引標籤的工具列上，按一下 [新增導出成員]。  
  
12. 在 **名稱**方塊中，變更此導出量值名稱`[Total GPM]`。  
  
13. 在 [運算式] 方塊中，建立下列 MDX 運算式：  
  
    ```  
    ([Measures].[Total Sales Amount] -   
    [Measures].[Total Product Cost]) /  
    [Measures].[Total Sales Amount]  
    ```  
  
     請注意，這個導出成員參考其他導出成員。 由於這個導出成員會在它所參考的導出成員之後導出，因此它是有效的導出成員。  
  
14. 在 [格式字串] 清單中，選取 [百分比]。  
  
15. 在 [非空白行為] 清單中，勾選 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
16. 在 [計算] 索引標籤的工具列上，按一下 [指令碼檢視]，然後檢閱您剛新增至計算指令碼中的三個計算值。  
  
17. 在計算指令碼前立即新增新的一行`[Internet GPM]`計算，然後將下列文字加入指令碼的那一行：  
  
    ```  
    /* Calculations to calculate gross profit margin */  
    ```  
  
     下圖顯示含有三個新計算值的 [運算式] 窗格。  
  
     ![在 [計算運算式] 窗格中的新計算](../../2014/tutorials/media/l6-calculatedmembers-05.gif "計算運算式窗格中的新計算")  
  
## <a name="defining-the-percent-of-total-calculations"></a>定義總計算值的百分比  
  
1.  在 [計算] 索引標籤的工具列上，按一下 [表單檢視]。  
  
2.  在 **指令碼組合管理**窗格中，選取`[Total GPM]`，然後按一下 [**新增導出成員**工具列上的**計算**] 索引標籤。  
  
     在按一下 [新增導出成員] 之前，先按一下 [指令碼組合管理] 窗格中的最後一個導出成員，可確保這個新的導出成員加在指令碼結尾。 指令碼是以它們出現在 [指令碼組合管理] 窗格中的順序執行的。  
  
3.  變更到這個新導出成員的名稱`[Internet Sales Ratio to All Products]`。  
  
4.  在 [運算式] 方塊中，輸入下列運算式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Internet Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Internet Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Internet Sales-Sales Amount] )  
        End  
    ```  
  
     這個 MDX 運算式會將比重計算為每項產品的總網際網路銷售值。 Case 陳述式與 IS EMPTY 函數，可以共同確保產品沒有銷售量時，並不會發生除以零的錯誤。  
  
5.  在 [格式字串] 清單中，選取 [百分比]。  
  
6.  在 [非空白行為] 清單中，勾選 [網際網路銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
7.  在 [計算] 索引標籤的工具列上，按一下 [新增導出成員]。  
  
8.  此導出成員的名稱變更`[Reseller Sales Ratio to All Products]`。  
  
9. 在 [運算式] 方塊中，輸入下列運算式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Reseller Sales-Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Reseller Sales-Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Reseller Sales-Sales Amount] )  
        End  
    ```  
  
10. 在 [格式字串] 清單中，選取 [百分比]。  
  
11. 在 [非空白行為] 清單中，勾選 [轉售商銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
12. 在 [計算] 索引標籤的工具列上，按一下 [新增導出成員]。  
  
13. 此導出成員的名稱變更`[Total Sales Ratio to All Products]`。  
  
14. 在 [運算式] 方塊中，輸入下列運算式：  
  
    ```  
    Case  
        When IsEmpty( [Measures].[Total Sales Amount] )   
        Then 0  
        Else ( [Product].[Product Categories].CurrentMember,  
               [Measures].[Total Sales Amount]) /  
             ( [Product].[Product Categories].[(All)].[All],   
               [Measures].[Total Sales Amount] )  
        End  
    ```  
  
15. 在 [格式字串] 清單中，選取 [百分比]。  
  
16. 在 [非空白行為] 清單中，勾選 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 的核取方塊，然後按一下 [確定]。  
  
17. 在 [計算] 索引標籤的工具列上，按一下 [指令碼檢視]，然後檢閱您剛新增至計算指令碼中的三個計算值。  
  
18. 在計算指令碼前立即新增新的一行`[Internet Sales Ratio to All Products]`計算，然後將下列文字加入指令碼的那一行：  
  
    ```  
    /* Calculations to calculate percentage of product to total product sales */  
    ```  
  
     您總共定義了八個導出成員，當您在表單檢視時，它們都會出現在 [指令碼組合管理] 窗格中。  
  
## <a name="browsing-the-new-calculated-members"></a>瀏覽新的導出成員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，切換到 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
3.  按一下 Excel 圖示，然後按一下 [啟用]。  
  
4.  在 [樞紐分析表欄位清單] 窗格中，展開 [值] 資料夾來檢視量值維度中的新導出成員。  
  
5.  將 [總銷售量] 拖曳至 [值] 區域中，然後檢閱結果。  
  
     從 [網際網路銷售] 和 [轉售商銷售] 量值群組，將 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 量值拖曳至 [值] 區域中。  
  
     請注意，[總銷售量] 量值是 [網際網路銷售 - 銷售量] 量值和 [轉售商銷售 - 銷售量] 量值的總和。  
  
6.  將 [產品類別目錄] 使用者定義階層新增至 [報表篩選] 區域的篩選區域，然後再依 [越野車] 篩選資料。  
  
     請注意，[總銷售量] 量值是根據 [越野車] 的 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 量值，針對產品銷售的 [越野車] 類別目錄而計算的。  
  
7.  將 **Date.Calendar Date** 使用者定義階層新增至 [資料列標籤] 區域，然後檢閱結果。  
  
     請注意，每個日曆年度的 [總銷售量] 量值，是以 [越野車] 的 [網際網路銷售 - 銷售量] 和 [轉售商銷售 - 銷售量] 量值為依據，並針對產品銷售的 [越野車] 類別目錄而計算的。  
  
8.  將 [總毛利率]、[網際網路毛利率] 和 [轉售商毛利率] 量值新增至 [值] 區域中，然後檢閱結果。  
  
     請注意，轉售商銷售的毛利率遠低於透過網際網路的銷售，如下圖所示。  
  
     ![顯示轉售商銷售的 [資料] 窗格](../../2014/tutorials/media/l6-calculatedmembers-7b.gif "顯示轉售商銷售的 [資料] 窗格")  
  
9. 將 [總銷售與所有產品的比率]、[網際網路銷售與所有產品的比率] 以及 [轉售商銷售與所有產品的比率] 量值新增至 [值] 區域中。  
  
     請注意，越野車銷售與所有產品的比率，在網際網路銷售方面正逐漸提升，不過在轉售商銷售方面卻有下滑趨勢。 另外也請注意，越野車銷售與所有產品的比率，透過轉售商的銷售，低於透過網際網路的銷售。  
  
10. 將篩選器從 [越野車] 改為 [自行車]，然後檢閱結果。  
  
     請注意，透過轉售商銷售的所有自行車毛利率是負值，因為休旅車和公路自行車是虧本出售。  
  
11. 將篩選器改為 [配件]，然後檢閱結果。  
  
     請注意，配件的銷售量逐漸上升中，但這些銷售在總銷售量中只佔一小部分。 另外也請注意，配件銷售的毛利率高於自行車的毛利率。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [定義命名集](../analysis-services/lesson-6-2-defining-named-sets.md)  
  
## <a name="see-also"></a>另請參閱  
 [計算](multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [多維度模型中的計算](multidimensional-models/calculations-in-multidimensional-models.md)   
 [建立導出成員](multidimensional-models/create-calculated-members.md)  
  
  
