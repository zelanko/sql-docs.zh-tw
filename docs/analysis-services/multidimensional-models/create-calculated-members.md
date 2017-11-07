---
title: "建立導出的成員 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculated members [Analysis Services]
- custom measures [Analysis Services]
- members [Analysis Services], calculated
- calculations [Analysis Services], calculated members
ms.assetid: 820e4b18-9c3a-4b12-a126-ca16d8364a00
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 73feb8d67594c4967fa0ecb0050783b970e58726
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-calculated-members"></a>建立導出成員
  您可以結合 Cube 資料、算術運算子、數字和函數，來建立自訂的量值或維度成員，稱為導出成員。 例如，您可以建立一個名為 Euros 的導出成員，藉由將現有的美金量值乘以轉換比率，來將美金轉換為歐元。 然後可以在另一個資料列或資料行中，向一般使用者顯示歐元。  
  
 導出成員定義將會被儲存，但是它們的值只存在於記憶體中。 在前述的範例中，會對一般使用者顯示歐元值但不會儲存為 Cube 資料。  
  
 您在 Cube 中建立導出成員。 若要建立導出成員，請在 Cube 設計師的 [計算] 索引標籤上，按一下工具列上的 [新增導出成員] 圖示。 此命令會顯示一個表單，以指定導出成員的下列選項：  
  
 **名稱**  
 選取導出成員的名稱。 當一般使用者瀏覽 Cube 時，此名稱會顯示為導出成員值的資料行或資料列標題。  
  
 **父階層**  
 選取要包含在導出成員中的父階層。 階層是維度的描述性類別目錄，利用階層即可將 Cube 中的數值資料 (亦即，量值) 分開以便分析。 在表格式瀏覽器中，階層會提供資料行和資料列標題，一般使用者瀏覽 Cube 中的資料時，會向一般使用者顯示這些標題。 (在圖形化瀏覽器中，階層會提供其他類型的描述性標籤，不過功能和表格式瀏覽器中相同。)導出成員在您所選取的父維度中提供新的標題 (或標籤)。  
  
 或者，您可以在量值中 (而非維度中) 包含導出成員。 此選項也會提供新資料行或資料列標題，但它會附加至瀏覽器中的量值。  
  
 **父成員**  
 按一下 [變更]，即可選取要包含導出成員的父成員。 如果您選取單層階層或 MEASURES 做為父維度，則無法使用此選項。  
  
 階層劃分為包含成員的層級。 每一個成員產生一個標題。 瀏覽 Cube 中的資料時，一般使用者可以從選取的標題，向下鑽研至先前未顯示的從屬標題。 導出成員的標題會直接加入在您所選取的父成員之下的層級。  
  
 **運算式**  
 指定產生導出成員之值的運算式。 此運算式可以使用多維度運算式 (MDX) 撰寫。 運算式可以包含下列任一項：  
  
-   顯示 Cube 元件的資料運算式，例如維度、層級、量值等等  
  
-   算術運算子  
  
-   數字  
  
-   函數  
  
 您可以從 [計算工具] 窗格的 [中繼資料] 索引標籤中，拖曳或複製 Cube 元件，以快速將這些元件加入至運算式。  
  
> [!IMPORTANT]  
>  導出成員若要用於另一個導出成員的值運算式中，就必須在使用該成員的導出成員之前建立。  
  
 格式字串  
 指定根據導出成員之資料格值的格式。 此屬性接受的值與量值的 **Display Format** 屬性相同。 如需有關顯示格式的詳細資訊，請參閱 [設定量值屬性](../../analysis-services/multidimensional-models/configure-measure-properties.md)。  
  
 Visible  
 決定擷取 Cube 中繼資料時是要看到或隱藏導出成員。 如果隱藏導出成員，則仍可將它用於 MDX 運算式、陳述式和指令碼，但是它在用戶端使用者介面中並不會顯示為可選取的物件。  
  
 非空白行為  
 儲存量值的名稱，用來在 MDX 中解析 NON EMPTY 查詢。 如果這個屬性空白，則必須重複評估導出成員來決定成員是否為空白。 如果這個屬性包含一或多個量值的名稱，則在所有指定的量值都為空白時，會將導出成員視為空白。 這個屬性是最佳化提示，要 Analysis Services 只傳回非 NULL 的記錄。 如果只傳回非 NULL 記錄，將會改善利用 NON EMPTY 運算子或 NonEmpty 函數或是必須計算資料格值之 MDX 查詢的效能。 為了在計算資料格時獲得最佳效能，請盡可能只指定單一成員。  
  
 色彩運算式  
 指定 MDX 運算式，以根據導出成員的值來動態設定資料格的前景和背景顏色。 如果用戶端應用程式不支援，則會忽略此屬性。  
  
 字型運算式  
 指定 MDX 運算式，以根據導出成員的值來動態設定資料格的字型、字型大小和字型屬性。 如果用戶端應用程式不支援，則會忽略此屬性。  
  
 您可以從 [計算工具] 窗格的 [中繼資料] 索引標籤中，複製或拖曳 Cube 元件至 [計算運算式] 窗格裡的 [運算式] 方塊。 您可以從 [計算工具] 窗格的 [函數] 索引標籤中，複製或拖曳函數至 [計算運算式] 窗格裡的 [運算式] 方塊。  
  
## <a name="addressing-calculated-members"></a>定址導出成員  
 您在 Cube 設計師的 [計算] 索引標籤上建立導出成員時，會指定要儲存導出成員的父階層。 父階層會依據下列規則決定如何定址導出成員：  
  
-   如果導出成員是建立在量值維度中，則導出成員可以在該維度中定址。  
  
## <a name="see-also"></a>請參閱＜  
 [Calculations in Multidimensional Models](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  

