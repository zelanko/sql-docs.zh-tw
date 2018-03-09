---
title: "修改 [產品] 維度 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8bbed44f2b02b0d94678513185dbf682a537e9e5
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="lesson-3-3---modifying-the-product-dimension"></a>課程 3-3-修改 [產品] 維度
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

在這個主題的工作中，您會使用具名計算來針對產品線提供更具描述性的名稱、定義 [產品] 維度中的階層，以及指定該階層的 (全部) 成員名稱。 此外，您也會將屬性分組放入顯示資料夾中。  
  
## <a name="adding-a-named-calculation"></a>加入具名計算  
您可以將具名計算加入至資料來源檢視中的資料表。 在下列工作中，您會建立可顯示完整產品線名稱的具名計算。  
  
#### <a name="to-add-a-named-calculation"></a>加入具名計算  
  
1.  若要開啟 [Adventure Works DW 2012] 資料來源檢視，請在方案總管的 [資料來源檢視] 資料夾中按兩下 [Adventure Works DW 2012]。  
  
2.  在 [圖表] 窗格的底部，以滑鼠右鍵按一下 [Product] 資料表標頭，然後按一下 [新增具名計算]。  
  
3.  在 [建立具名計算] 對話方塊中，於 [資料行名稱] 方塊中輸入 **ProductLineName**。  
  
4.  在 [運算式] 方塊中，輸入或複製並貼上下列 **CASE** 陳述式：  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
    這個 **CASE** 陳述式會為 Cube 的每個產品線建立使用者易記名稱。  
  
5.  按一下 [確定] 建立 [ProductLineName] 具名計算。 您可能需要稍等一下。  
  
6.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>修改屬性 (Attribute) 的 NameColumn 屬性 (Property)  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>修改屬性 (Attribute) 的 NameColumn 屬性 (Property)  
  
1.  針對 [產品] 維度切換到維度設計師。 若要這樣做，請在方案總管的 [維度] 節點中，按兩下 [產品] 維度。  
  
2.  在 [維度結構] 索引標籤的 [屬性] 窗格中，選取 [產品線]。  
  
3.  在畫面右側的 [屬性] 視窗中，按一下視窗底部的 **NameColumn** 屬性欄位，然後按一下瀏覽 (**...**) 按鈕，即可開啟 [名稱資料行] 對話方塊。 (您可能需要按一下畫面右側的 [屬性] 索引標籤開啟 [屬性] 視窗)。  
  
4.  選取 [來源資料行] 清單底部的 [ProductLineName]，然後按一下 [確定]。  
  
    [NameColumn] 欄位現在會包含 **Product.ProductLineName (WChar)** 文字。 [產品線] 屬性階層的成員現在會顯示產品線的全名，而非產品線的簡稱。  
  
5.  在 [維度結構] 索引標籤的 [屬性] 窗格中，選取 [產品金鑰]。  
  
6.  在 [屬性] 視窗中按一下 [NameColumn] 屬性欄位，然後按一下省略符號瀏覽 (**...**) 按鈕，即可開啟 [名稱資料行] 對話方塊。  
  
7.  選取 [來源資料行] 清單中的 [EnglishProductName]，然後按一下 [確定]。  
  
    [NameColumn] 欄位現在會包含 **Product.EnglishProductName (WChar)** 文字。  
  
8.  在 [屬性] 視窗中向上捲動，按一下 [Name] 屬性欄位，然後輸入 [產品名稱]。  
  
## <a name="creating-a-hierarchy"></a>建立階層  
  
#### <a name="to-create-a-hierarchy"></a>若要建立階層  
  
1.  將 [產品線] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格中。  
  
2.  將 [型號名稱] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [產品線] 層級底下)。  
  
3.  將 [產品名稱] 屬性從 [屬性] 窗格拖曳到 [階層] 窗格的 [<new level>] 資料格中 (位於 [型號名稱] 層級底下)。 您在上一節中已將 [產品金鑰] 重新命名為 [產品名稱]。  
  
4.  在 [維度結構] 索引標籤的 [階層] 窗格中，以滑鼠右鍵按一下 [階層] 階層的標題列，按一下 [重新命名]，然後輸入 [產品型號線]。  
  
    這個階層的名稱現在變成 [產品型號線]。  
  
5.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="specifying-folder-names-and-all-member-names"></a>指定資料夾名稱和所有成員名稱  
  
#### <a name="to-specify-the-folder-and-member-names"></a>若要指定資料夾名稱和成員名稱  
  
1.  在 [屬性] 窗格中，按住 CTRL 鍵，同時按一下每個屬性，藉以選取下列屬性：  
  
    -   **類別**  
  
    -   **Color**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **大小**  
  
    -   **Size Range**  
  
    -   **樣式**  
  
    -   **Weight**  
  
2.  在 [屬性] 視窗的 [AttributeHierarchyDisplayFolder] 屬性欄位中，輸入 [庫存]。  
  
    現在您已將這些屬性分組放入單一顯示資料夾。  
  
3.  在 [屬性] 窗格中，選取下列屬性：  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  在 [屬性] 視窗的 [AttributeHierarchyDisplayFolder] 屬性資料格中，輸入 [財務]。  
  
    現在您已將這些屬性分組放入第二個顯示資料夾。  
  
5.  在 [屬性] 窗格中，選取下列屬性：  
  
    -   **End Date**  
  
    -   **開始日期**  
  
    -   **狀態**  
  
6.  在 [屬性] 視窗的 [AttributeHierarchyDisplayFolder] 屬性資料格中，輸入 [歷史]。  
  
    現在您已將這些屬性分組放入第三個顯示資料夾。  
  
7.  在 [階層] 窗格中，選取 [產品型號線] 階層，然後將 [屬性] 視窗中的 **AllMemberName** 屬性變更為 [所有產品]。  
  
8.  按一下 [階層] 窗格中的開放區域，然後將 [屬性] 視窗頂部的 **AttributeAllMemberName** 屬性變更為 [所有產品]。  
  
    按一下開放區域可讓您修改 [Product] 維度本身的屬性。 您也可以在 [屬性] 窗格中，按一下屬性清單最上方的 [Product]。  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-attribute-relationships"></a>定義屬性關聯性  
如果基礎資料支援屬性關聯性，您就應該定義屬性之間的屬性關聯性。 定義屬性關聯性可加快維度、資料分割和查詢處理的速度。 如需詳細資訊，請參閱 [定義屬性關聯性](../analysis-services/multidimensional-models/attribute-relationships-define.md) 和 [屬性關聯性](../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
#### <a name="to-define-attribute-relationships"></a>定義屬性關聯性  
  
1.  在 [產品] 維度的 [維度設計師] 中，按一下 [屬性關聯性] 索引標籤。  
  
2.  在圖表中，以滑鼠右鍵按一下 [型號名稱] 屬性，然後按一下 [新增屬性關聯性]。  
  
3.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [型號名稱]。 將 [相關屬性] 設定為 [產品線]。  
  
    然後，在 [關聯性類型] 清單中，保持關聯性類型設定為 [彈性] 的狀態，因為成員之間的關聯性可能會隨著時間而變更。 例如，產品型號最後可能會移至不同的產品線。  
  
4.  按一下 **[確定]**。  
  
5.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="reviewing-product-dimension-changes"></a>檢閱 Product 維度變更  
  
#### <a name="to-review-the-product-dimension-changes"></a>若要檢閱 Product 維度變更  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  當您收到 [已成功地完成部署] 訊息之後，請針對 [產品] 維度按一下 [維度設計師] 的 [瀏覽器] 索引標籤，然後按一下設計師工具列上的 [重新連接] 圖示。  
  
3.  確認已在 [階層] 清單中選取 [產品型號線]，然後展開 [所有產品]。  
  
    請注意，[全部] 成員的名稱會顯示成 [所有產品]。 這是因為您在本課程的前面，將階層的 **AllMemberName** 屬性變更為 [所有產品]。 此外，[產品線] 層級的成員現在有了使用者易記名稱，而非單一字母的縮寫。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[修改 Date 維度](../analysis-services/lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>另請參閱  
[在資料來源檢視 &#40; 中定義具名的計算Analysis Services &#41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
[建立使用者定義階層](../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
[設定屬性階層的 &#40;全部&#41; 層級](../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
