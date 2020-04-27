---
title: 修改客戶維度 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2530d42c70b506fe927d35fd4e6f862e22e1ea1a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078933"
---
# <a name="modifying-the-customer-dimension"></a>修改 [客戶] 維度
  您有許多不同方式可以增加 Cube 中維度的可用性和功能性。 在這個主題的工作中，您會修改 Customer 維度。  
  
## <a name="renaming-attributes"></a>重新命名屬性  
 您可以使用 [維度設計師] 的 [維度結構]**** 索引標籤來變更屬性名稱。  
  
#### <a name="to-rename-an-attribute"></a>重新命名屬性  
  
1.  針對 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的 [客戶] 維度，切換至 [維度設計師]****。 若要這樣做，請在方案總管的 [維度]**** 節點中，按兩下 [客戶]**** 維度。  
  
2.  在 [屬性]**** 窗格中，以滑鼠右鍵按一下 [英文國家地區名稱]****，然後按一下 [重新命名]****。 將屬性的名稱變更為`Country-Region`。  
  
3.  請以相同方式變更下列屬性的名稱：  
  
    -   **英文教育**屬性-變更為`Education`  
  
    -   **美式職業**屬性-變更為`Occupation`  
  
    -   **州/省名稱**屬性-變更為`State-Province`  
  
4.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="creating-a-hierarchy"></a>建立階層  
 您可以將屬性從 [屬性]**** 窗格拖曳到 [階層]**** 窗格，藉以建立新的階層。  
  
#### <a name="to-create-a-hierarchy"></a>若要建立階層  
  
1.  將`Country-Region`屬性從 [**屬性**] 窗格拖曳到 [**階層] 窗格**中。  
  
2.  將`State-Province`屬性從 [**屬性**] 窗格拖曳**到 [階層**] 窗格的 [ ** \<新增層級**]>`Country-Region`資料格（在層級底下）。  
  
3.  將 [ **City** ] 屬性從 [**屬性**] 窗格拖曳到 [**階層] 窗格**中的 [ ** \<新增層級]>** 資料格（在`State-Province`層級底下）。  
  
4.  在 [**維度結構**] 索引卷**標的 [階層] 窗格中**，以滑鼠右鍵按一下階層**階層的標題**欄，選取 [ `Customer Geography`**重新命名**]，然後輸入。  
  
     階層的名稱現在`Customer Geography`是。  
  
5.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="adding-a-named-calculation"></a>加入具名計算  
 具名計算是以導出資料行表示的 SQL 運算式，您可以將它加入資料來源檢視的資料表中。 這個運算式以資料表的資料行呈現及運作。 具名計算可讓您延伸資料來源檢視中現有資料表的關聯式結構描述，而不必修改基礎資料來源中的資料表。 如需詳細資訊，請參閱[在資料來源 View 中定義指名的計算 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>加入具名計算  
  
1.  在方案總管的**資料來源 Views**資料夾中按兩下，以開啟** [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012**資料來源 view。  
  
2.  在左側的 [資料表]**** 窗格中，以滑鼠右鍵按一下 [客戶]****，然後按一下 [新增具名計算]****。  
  
3.  在 [**建立命名計算**] 對話方塊中， `FullName`于 [資料**行名稱**] 方塊中輸入，然後在 [**運算式**] `CASE`方塊中輸入或複製並貼上下列語句：  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     `CASE`語句會將**FirstName**、 **MiddleName**和**LastName**資料行串連成單一資料行，您將在 [客戶] 維度中用來當做**customer**屬性的顯示名稱。  
  
4.  按一下 [確定]****，然後展開 [資料表]**** 窗格中的 [客戶]****。  
  
     `FullName`已命名的計算會出現在 Customer 資料表的資料行清單中，並以圖示表示它是名為的計算。  
  
5.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
6.  在 [資料表]**** 窗格中，以滑鼠右鍵按一下 [客戶]****，然後按一下 [瀏覽資料]****。  
  
7.  檢閱 [瀏覽客戶資料表]**** 檢視中的最後一個資料行。  
  
     `FullName`請注意，資料行會出現在 [資料來源] 視圖中，將資料從基礎資料來源中的數個數據行正確串連，而不需要修改原始資料來源。  
  
8.  關閉 [瀏覽 Customer 資料表]**** 索引標籤。  
  
## <a name="using-the-named-calculation-for-member-names"></a>針對成員名稱使用具名計算  
 在資料來源檢視中建立具名計算之後，您就可以使用此具名計算當做屬性 (Attribute) 的屬性 (Property)。  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>針對成員名稱使用具名計算  
  
1.  針對 [客戶] 維度切換到維度設計師。  
  
2.  在 [維度結構]**** 索引標籤的 [屬性]**** 窗格中，按一下 [客戶索引鍵]**** 屬性。  
  
3.  開啟 [屬性] 視窗，然後按一下標題列上的 [自動隱藏]**** 按鈕，如此它就會保持開啟狀態。  
  
4.  在 [**名稱**] 屬性欄位中`Full Name`，輸入。  
  
5.  按一下底部的 [ **NameColumn** ] 屬性欄位，然後按一下 [流覽] （**...**）按鈕，即可開啟 [名稱資料**行**] 對話方塊。  
  
6.  選取`FullName` [**來源資料行**] 清單底部的，然後按一下 **[確定]**。  
  
7.  在 [維度結構] 索引標籤`Full Name`中，將屬性從 [**屬性**] 窗格拖曳**到 [階層] 窗格**中 [ **City** ] 層級下的 [ ** \<新增層級>** ] 資料格。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-display-folders"></a>定義顯示資料夾  
 您可以使用顯示資料夾，將使用者和屬性階層分組放到資料夾結構中，以便提高可用性。  
  
#### <a name="to-define-display-folders"></a>若要定義顯示資料夾  
  
1.  針對 [客戶] 維度開啟 [維度結構]**** 索引標籤。  
  
2.  在 [屬性]**** 窗格中，按住 CTRL 鍵，同時按一下每個屬性，藉以選取下列屬性：  
  
    -   **城市**  
  
    -   `Country-Region`  
  
    -   **Postal Code**  
  
    -   `State-Province`  
  
3.  在 [屬性視窗中，按一下頂端的 [ **attributehierarchydisplayfolder]** ] 屬性欄位（您可能需要指向它以查看完整名稱），然後輸入`Location`。  
  
4.  在 [**階層] 窗格**中`Customer Geography`，按一下 []，然後在右邊的 [屬性視窗`Location`中，選取做為**DisplayFolder**屬性的值。  
  
5.  在 [屬性]**** 窗格中，按住 CTRL 鍵，同時按一下每個屬性，藉以選取下列屬性：  
  
    -   **Commute Distance**  
  
    -   `Education`  
  
    -   **性別**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   `Occupation`  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  在 [屬性視窗中，按一下頂端的 [ **attributehierarchydisplayfolder]** ] 屬性欄位，然後輸入`Demographic`。  
  
7.  在 [屬性]**** 窗格中，按住 CTRL 鍵，同時按一下每個屬性，藉以選取下列屬性：  
  
    -   **電子郵件地址**  
  
    -   **來電**  
  
8.  在 [屬性視窗中，按一下 [ **attributehierarchydisplayfolder]** ] 屬性欄位`Contacts`，然後輸入。  
  
9. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-composite-keycolumns"></a>定義複合 KeyColumns  
 [KeyColumns]**** 屬性 (property) 包含代表屬性 (attribute) 之索引鍵的一或多個資料行。 在這一課，您會建立**城市**和`State-Province`屬性的複合索引鍵。 當您需要唯一識別某個屬性時，複合索引鍵便很有用。 例如，當您稍後在本教學課程中定義屬性關聯性時， **City**屬性必須唯一`State-Province`識別屬性。 不過，不同省份可能會有許多相同名稱的縣 (市) 存在。 因此，您將建立由 [縣 (市)]**** 屬性之 [StateProvinceName]**** 和 [City]**** 資料行所組成的複合索引鍵。 如需詳細資訊，請參閱 [修改屬性 (Attribute) 的 KeyColumn 屬性 (Property)](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)。  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>針對 [縣 (市)] 屬性定義複合 KeyColumns  
  
1.  針對 [客戶] 維度開啟 [維度結構]**** 索引標籤。  
  
2.  在 [屬性]**** 窗格中，按一下 [縣 (市)]**** 屬性。  
  
3.  在 [屬性]**** 視窗中靠近底部的 [KeyColumns]**** 欄位中按一下，然後按一下瀏覽 (**...**) 按鈕。  
  
4.  在 [索引鍵資料行]**** 對話方塊的 [可用的資料行]**** 清單中，選取 [StateProvinceName]**** 資料行，然後按一下 [>]**** 按鈕。  
  
     [City]**** 和 [StateProvinceName]**** 資料行現在會顯示在 [索引鍵資料行]**** 清單中。  
  
5.  按一下 [確定]  。  
  
6.  若要設定 [縣 (市)]**** 屬性 (attribute) 的 [NameColumn]**** 屬性 (property)，請按一下 [屬性] (property) 視窗中的 [NameColumn]**** 欄位，然後按一下瀏覽 (**...**) 按鈕。  
  
7.  在 [名稱資料行]**** 對話方塊的 [來源資料行]**** 清單中，選取 [City]****，然後按一下 [確定]****。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>針對 [省份] 屬性定義複合 KeyColumns  
  
1.  請確定 [客戶] 維度的 [維度結構]**** 索引標籤為開啟狀態。  
  
2.  在 [**屬性**] 窗格中， `State-Province`按一下屬性。  
  
3.  在 [屬性]**** 視窗的 [KeyColumns]**** 欄位中按一下，然後按一下瀏覽 (**...**) 按鈕。  
  
4.  在 [索引鍵資料行]**** 對話方塊的 [可用的資料行]**** 清單中，選取 [EnglishCountryRegionName]**** 資料行，然後按一下 [>]**** 按鈕。  
  
     [EnglishCountryRegionName]**** 和 [StateProvinceName]**** 資料行現在會顯示在 [索引鍵資料行]**** 清單中。  
  
5.  按一下 [確定]  。  
  
6.  若要設定**NameColumn** `State-Province`屬性的 namecolumn 屬性，請按一下 [屬性視窗中的 [ **namecolumn** ] 欄位，然後按一下 [流覽] （**...**）按鈕。  
  
7.  在 [名稱資料行]**** 對話方塊的 [來源資料行]**** 清單中，選取 [StateProvinceName]****，然後按一下 [確定]****。  
  
8.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="defining-attribute-relationships"></a>定義屬性關聯性  
 如果基礎資料支援屬性關聯性，您就應該定義屬性之間的屬性關聯性。 定義屬性關聯性可加快維度、資料分割和查詢處理的速度。 如需詳細資訊，請參閱 [定義屬性關聯性](multidimensional-models/attribute-relationships-define.md) 和 [屬性關聯性](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)。  
  
#### <a name="to-define-attribute-relationships"></a>定義屬性關聯性  
  
1.  在 [客戶] 維度的 [**維度設計師**] 中，按一下 [**屬性關聯**性] 索引標籤。您可能需要等待。  
  
2.  在圖表中，以滑鼠右鍵按一下 [縣 (市)]**** 屬性，然後按一下 [新增屬性關聯性]****。  
  
3.  在 [建立屬性關聯性]**** 對話方塊中，[來源屬性]**** 是 [縣 (市)]****。 將**相關屬性**設定為`State-Province`。  
  
4.  在 [關聯性類型]**** 清單中，將關聯性類型設定為 [固定]****。  
  
     此關聯性類型是 [固定]****，因為成員之間的關聯性不會隨著時間而變更。 例如，某個縣 (市) 成為不同省份一部分的情況並不常見。  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  在圖表中，以滑鼠右鍵按一下`State-Province`屬性，然後選取 [**新增屬性關聯**性]。  
  
7.  在 [**建立屬性關聯**性] 對話方塊中，[**來源屬性**] 是`State-Province`。 將**相關屬性**設定為`Country-Region`。  
  
8.  在 [關聯性類型]**** 清單中，將關聯性類型設定為 [固定]****。  
  
9. 按一下 [確定]  。  
  
10. 按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>部署變更、處理物件及檢視變更  
 在變更屬性和階層之後，您必須部署變更及重新處理相關物件，然後才可以檢視變更。  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>部署變更、處理物件及檢視變更  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的 [建立]**** 功能表上，按一下 [部署 Analysis Services 教學課程]****。  
  
2.  當您收到 [已成功地完成部署]**** 訊息之後，請針對 [客戶] 維度按一下 [維度設計師] 的 [瀏覽器]**** 索引標籤，然後按一下設計師工具列左側的 [重新連接] 按鈕。  
  
3.  `Customer Geography`確認已在 [階層]**清單中**選取，然後在瀏覽器窗格中展開 [**全部**]，展開 [**澳大利亞**]，展開 [**新南威爾士**]，然後展開 [ **Coffs Harbour**]。  
  
     瀏覽器就會顯示該縣 (市) 的客戶。  
  
4.  針對 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 切換至 [Cube 設計師]****。 若要這樣做，請在**方案總管**的 [Cube]**** 節點中，按兩下 [Analysis Services 教學課程]**** Cube。  
  
5.  按一下 [瀏覽器]**** 索引標籤，然後按一下設計師工具列上的 [重新連接] 按鈕。  
  
6.  在 [量值群組]**** 窗格中，展開 [客戶]****。  
  
     請注意，出現在 [客戶] 底下的只有顯示資料夾和不含顯示資料夾值的屬性，而非冗長的屬性清單。  
  
7.  按一下 [ **檔案** ] 功能表上的 [ **全部儲存**]。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [修改產品維度](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>另請參閱  
 [維度屬性屬性參考](multidimensional-models/dimension-attribute-properties-reference.md)   
 [從維度中移除屬性](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [重新命名屬性](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [在資料來源檢視中定義具名計算 &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
