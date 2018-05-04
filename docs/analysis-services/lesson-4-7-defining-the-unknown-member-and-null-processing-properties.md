---
title: 定義未知的成員和 Null 處理屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: d9abb09c-9bfa-4e32-b530-8590e4383566
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5d59f09c5f227f684103434ae4371d4b41379482
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-4-7---defining-the-unknown-member-and-null-processing-properties"></a>課程 4-7-定義未知的成員和 Null 處理屬性
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

當 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 處理維度時，資料來源檢視中之資料表或檢視內基礎資料行的所有相異值會在維度中擴展屬性。 如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在處理期間發現 Null 值，它預設會將這個 Null 轉換成零 (若為數值資料行) 或空字串 (若為字串資料行)。 您可以在基礎關聯式資料倉儲的擷取、轉換和載入過程中，修改這些預設值或轉換 Null 值 (如果有的話)。 此外，您也可以設定下列三個屬性，藉以讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 將 Null 值轉換成指定的值：維度的 [UnknownMember] 和 [UnknownMemberName] 屬性 (property)，以及維度索引鍵屬性 (attribute) 的 [NullProcessing] 屬性 (property)。  
  
「維度精靈」和「Cube 精靈」將會根據維度的索引鍵屬性是否可為 Null，或者雪花維度的根屬性是否以可為 Null 的資料行為基礎，自動為您啟用這些屬性。 在這些情況下，索引鍵屬性 (attribute) 的 [NullProcessing] 屬性 (property) 將會設定為 [UnknownMember]，而 [UnknownMember] 屬性 (property) 則會設定為 [可見]。  
  
但是，當您以累加方式建立雪花維度時 (就如同我們在這個教學課程中處理 [產品] 維度的方式一樣)，或者當您使用 [維度設計師] 定義維度，然後將這些現有的維度合併到 Cube 中時，可能必須以手動方式設定 [UnknownMember] 和 [NullProcessing] 屬性。  
  
在這個主題的工作中，您會從雪花資料表將產品類別目錄和產品子類別目錄屬性加入 [產品] 維度中，而且您將把雪花資料表加入 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 資料來源檢視中。 接著，您會為 [產品] 維度啟用 [UnknownMember] 屬性 (property)、指定 [組件元件] 當作 [UnknownMemberName] 屬性 (property) 的值、使 [子類別目錄] 和 [類別目錄] 屬性 (attribute) 與產品名稱屬性 (attribute) 產生關聯，然後為連結雪花資料表的成員索引鍵屬性 (attribute) 定義自訂的錯誤處理方式。  
  
> [!NOTE]  
> 如果您最初使用「Cube 精靈」定義 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 教學課程 Cube 時已經加入了 [子類別目錄] 和 [類別目錄] 屬性，系統就會自動執行這些步驟。  
  
## <a name="reviewing-error-handling-and-unknown-member-properties-in-the-product-dimension"></a>在 [產品] 維度中檢閱錯誤處理方式和未知的成員屬性  
  
1.  請針對 [產品] 維度切換到 [維度設計師]，按一下 [維度結構] 索引標籤，然後在 [屬性] 窗格中選取 [產品]。  
  
    這可讓您檢視及修改維度本身的屬性。  
  
2.  在 [屬性] 視窗中，檢閱 [UnknownMember] 和 [UnknownMemberName] 屬性。  
  
    請注意，[UnknownMember] 屬性並未啟用，因為它的值是設定為 [無]，而不是 [可見] 或 [隱藏]，而且沒有為 [UnknownMemberName] 屬性指定任何名稱。  
  
3.  在 [屬性] 視窗的 [ErrorConfiguration] 屬性資料格中選取 [(自訂)]，然後展開 [ErrorConfiguration] 屬性集合。  
  
    將 [ErrorConfiguration] 屬性設定為 [(自訂)]，可讓您檢視預設的錯誤組態設定，這麼做並不會變更任何設定。  
  
4.  檢閱索引鍵和 Null 索引鍵錯誤組態屬性，但不做任何變更。  
  
    請注意，依預設，當 Null 索引鍵轉換成未知的成員時，會忽略與這項轉換相關的處理錯誤。  
  
    下圖顯示 [ErrorConfiguration] 屬性集合的屬性設定。  
  
    ![ErrorConfiguration 屬性集合](../analysis-services/media/l4-productdimensionerrorconfig-1.gif "ErrorConfiguration 屬性集合")  
  
5.  按一下 [瀏覽器] 索引標籤，確認已在 [階層] 清單中選取 [產品型號線]，再展開 [所有產品]。  
  
    請注意 [產品線] 層級的 5 個成員。  
  
6.  依序展開 [元件] 和 [模型名稱] 層級的未標記成員。  
  
    這個層級包含在建立其他元件時所使用的組件元件，從 [Adjustable Race] 產品開始，如下圖所示。  
  
    ![用來建立其他元件的組件元件](../analysis-services/media/l4-productdimensionerrorconfig-2.gif "用來建立其他元件的組件元件")  
  
## <a name="defining-attributes-from-snowflaked-tables-and-a-product-category-user-defined-hierarchy"></a>定義雪花資料表中的屬性和產品類別目錄使用者定義階層  
  
1.  請針對 [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 資料來源檢視，開啟 [資料來源檢視設計工具]，選取 [圖表組合管理] 窗格中的 [轉售商銷售]，然後按一下 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的 [資料來源檢視] 功能表中的 [加入/移除物件]。  
  
    此時會開啟 [加入/移除資料表] 對話方塊。  
  
2.  在 [包含的物件] 清單中，選取 [DimProduct (dbo)]，然後按一下 [加入相關資料表]。  
  
    [DimProductSubcategory (dbo)] 和 [FactProductInventory (dbo)] 隨即加入。 移除 [FactProductInventory (dbo)]，只將 [DimProductSubcategory (dbo)] 資料表加入 [包含的物件] 清單。  
  
3.  預設選取 [DimProductSubcategory (dbo)] 資料表作為最新加入的資料表之後，再按一次 [加入相關資料表]。  
  
    此時會將 [DimProductCategory (dbo)] 資料表加入 [包含的物件] 清單。  
  
4.  按一下 **[確定]**。  
  
5.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的 [格式] 功能表中，指向 [自動配置]，然後按一下 [圖表]。  
  
    請注意，[DimProductSubcategory (dbo)] 資料表和 [DimProductCategory (dbo)] 資料表彼此連結，並且透過 [Product] 資料表連結到 [ResellerSales] 資料表。  
  
6.  請針對 [產品] 維度切換到 [維度設計師]，然後按一下 [維度結構] 索引標籤。  
  
7.  以滑鼠右鍵按一下 [資料來源檢視] 窗格中的任何位置，然後按一下 [顯示所有資料表]。  
  
8.  在 [資料來源檢視] 窗格中，尋找 [DimProductCategory] 資料表，以滑鼠右鍵按一下該資料表中的 [ProductCategoryKey]，然後按一下 [從資料行新增屬性]。  
  
9. 在 [屬性] 窗格中，將這個新屬性的名稱變更為**類別目錄**。  
  
10. 在 [屬性] 視窗的 [NameColumn] 屬性欄位中按一下，然後按一下瀏覽 (**…**) 按鈕，即可開啟 [名稱資料行] 對話方塊。  
  
11. 選取 [來源資料行] 清單中的 [EnglishProductCategoryName]，然後按一下 [確定]。  
  
12. 在 [資料來源檢視] 窗格中，尋找 [DimProductSubcategory] 資料表，以滑鼠右鍵按一下該資料表中的 [ProductSubcategoryKey]，然後按一下 [從資料行新增屬性]。  
  
13. 在 [屬性] 窗格中，將這個新屬性的名稱變更為**子類別目錄**。  
  
14. 在 [屬性] 視窗的 [NameColumn] 屬性欄位中按一下，然後按一下瀏覽 (**…**) 按鈕，即可開啟 [名稱資料行] 對話方塊。  
  
15. 選取 [來源資料行] 清單中的 [EnglishProductSubcategoryName]，然後按一下 [確定]。  
  
16. 建立稱為 [產品類別目錄] 的新使用者定義階層，其中含有下列層級，由上往下依序為：[類別目錄]、[子類別目錄] 和 [產品名稱]。  
  
17. 指定 [所有產品] 作為 [產品類別目錄] 使用者定義階層之 [AllMemberName] 屬性的值。  
  
## <a name="browsing-the-user-defined-hierarchies-in-the-product-dimension"></a>在產品維度中瀏覽使用者定義階層  
  
1.  在 [產品] 維度的 [維度設計師] 的 [維度結構] 索引標籤的工具列上，按一下 [處理]。  
  
2.  按一下 [是] 建立及部署專案，然後按一下 [執行] 處理 [產品] 維度。  
  
3.  處理成功之後，在 [處理進度] 對話方塊中依序展開 [Processing Dimension 'Product' completed successfully (產品維度已順利處理完成)]、[Processing Dimension Attribute 'Product Name' completed (產品名稱維度屬性已處理完成)] 和 [SQL 查詢 1]。  
  
4.  按一下 SELECT DISTINCT 查詢，然後按一下 [檢視詳細資料]。  
  
    請注意，WHERE 子句已加入 SELECT DISTINCT 子句中，它會移除在 ProductSubcategoryKey 資料行中沒有值的那些產品，如下圖所示。  
  
    ![顯示 WHERE 子句的 SELECT DISTINCT 子句](../analysis-services/media/l4-productnametraceline-1.gif "顯示 WHERE 子句的 SELECT DISTINCT 子句")  
  
5.  按三次 [關閉] 來關閉所有處理中的對話方塊。  
  
6.  請針對 [產品] 維度按一下 [維度設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
7.  確認 [產品型號線] 有出現在 [階層] 清單中，然後依序展開 [所有產品] 和 [元件]。  
  
8.  選取 [階層] 清單中的 [產品類別目錄]，依序展開 [所有產品] 和 [元件]。  
  
    請注意，沒有任何組件元件出現。  
  
若要修改上一項工作中提到的行為，您需要啟用 [產品] 維度的 [UnknownMember] 屬性、設定 [UnknownMemberName] 屬性的值、將 [子類別目錄] 和 [模型名稱] 屬性的 [NullProcessing] 屬性設定為 [UnknownMember]、將 [類別目錄] 屬性定義為 [子類別目錄] 屬性的相關屬性，然後將 [產品線] 屬性定義為 [模型名稱] 屬性的相關屬性。 這些步驟將會使 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在沒有 [SubcategoryKey] 資料行值的每一項產品中使用未知的成員名稱值，如下一項工作所示。  
  
## <a name="enabling-the-unknown-member-defining-attribute-relationships-and-specifying-custom-processing-properties-for-nulls"></a>啟用未知的成員、定義屬性關聯性及指定 Null 的自訂處理屬性  
  
1.  在 [產品] 維度的 [維度設計師] 中，按一下 [維度結構] 索引標籤，然後在 [屬性] 窗格中選取 [產品]。  
  
2.  在 [屬性] 視窗中，將 [UnknownMember] 屬性變更為 [可見]，再將 [UnknownMemberName] 屬性值變更為 [組件元件]。  
  
    將 [UnknownMember] 屬性變更為 [可見] 或 [隱藏] 會啟用維度的 [UnknownMember] 屬性。  
  
3.  按一下 **[屬性關聯性]** 索引標籤。  
  
4.  在圖表中，以滑鼠右鍵按一下 [子類別目錄] 屬性，然後選取 [新增屬性關聯性]。  
  
5.  在 [建立屬性關聯性] 對話方塊中，[來源屬性] 是 [子類別目錄]。 將 [相關屬性] 設定為 [類別目錄]。 然後，保持關聯性類型設定為 [彈性]。  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  在 [屬性] 窗格中，選取 [子類別目錄]。  
  
8.  在 [屬性] 視窗中，展開 [KeyColumns] 屬性，然後展開 [DimProductSubcategory.ProductSubcategoryKey (Integer)] 屬性。  
  
9. 將 [NullProcessing] 屬性變更為 [UnknownMember]。  
  
10. 在 [屬性] 窗格中，選取 [模型名稱]。  
  
11. 在 [屬性] 視窗中，展開 [KeyColumns] 屬性，然後展開 [Product.ModelName (WChar)] 屬性。  
  
12. 將 [NullProcessing] 屬性變更為 [UnknownMember]。  
  
    由於這些變更，當 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在處理期間發現 [子類別目錄] 屬性或 [模型名稱] 屬性是 Null 值時，未知的成員值會替換成索引鍵值，而使用者定義階層將可正確建構。  
  
## <a name="browsing-the-product-dimension-again"></a>再次瀏覽 [產品] 維度  
  
1.  在 [建立] 功能表上，按一下 [部署 Analysis Services 教學課程]。  
  
2.  順利完成部署之後，針對 [產品] 維度按一下 [維度設計師] 的 [瀏覽器] 索引標籤，然後按一下 [重新連接]。  
  
3.  確認已在 [階層] 清單中選取 [產品類別目錄]，然後展開 [所有產品]。  
  
    請注意，此時「組件元件」會出現成為 [類別目錄] 層級的新成員。  
  
4.  展開 [類別目錄] 層級的 [組件元件] 成員，然後展開 [子類別目錄] 層級的 [組件元件] 成員。  
  
    請注意，所有組件元件現在都會出現在 [產品名稱] 層級，如下圖所示。  
  
    ![顯示組件元件的產品名稱層級](../analysis-services/media/l4-assemblycomponents-1.gif "顯示組件元件的產品名稱層級")  
  
## <a name="next-lesson"></a>下一課  
[第 5 課： 定義維度與量值群組之間的關聯性](../analysis-services/lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)  
  
  
  
