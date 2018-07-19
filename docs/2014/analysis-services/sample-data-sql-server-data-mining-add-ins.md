---
title: 範例資料 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- holdout
- testing cases
- training cases
- partitioning data [data mining]
- mining models, testing
ms.assetid: 35907ae6-887f-4cb3-a750-cff3d7683d90
caps.latest.revision: 26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5984bbbaa3dc2bb55ce8f20a59dd5132de0ca72a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178965"
---
# <a name="sample-data-sql-server-data-mining-add-ins"></a>取樣資料 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的資料分割資料精靈](media/dmc-partition.gif "資料採礦功能區中的資料分割資料精靈")  
  
 **範例資料**精靈可讓您輕鬆地將您的來源資料分割成兩個集合，一個用於建立 （訓練） 模型，另一個用於測試模型。 此精靈也提供一個重新進行資料取樣的選項，藉以建立一個更能代表您目標的新資料集。  
  
 為定型和測試模型而建立正確類型的資料是資料採礦的一個重要部分，但是如果沒有正確的工具，也是會乏味無趣。 精靈會執行分層取樣，確保訓練和測試集之間對稱。  
  
## <a name="random-sampling-and-oversampling"></a>隨機取樣與超取樣  
 執行個體時提供 SQL Server 登入。 隨機取樣是確保您用於測試模型的資料能夠清楚代表您用於建立模型之資料的絕佳方式。 您可以隨機取樣存放在 Excel 中或外部資料來源中的資料  
  
 如果您使用隨機取樣選項，**範例資料**精靈會自動建立定型和測試資料集，並將其輸出到個別的 Excel 工作表，供日後參考。  
  
 如果您的資料儲存在 Excel 活頁簿，並不是外部資料來源，您也可以使用*超取樣*。 使用此選項時，您會指定一個在資料中可能很少見的目標值，精靈將會收集包含較多目標值的對稱集。 您可以導引精靈達成目標百分比，或建立特定數目的資料列。  
  
 如果您使用超取樣選項，**範例資料**精靈會建立新的工作表，其中包含新對稱的範例資料。  
  
## <a name="using-the-sample-data-wizard"></a>使用取樣資料精靈  
  
#### <a name="to-separate-data-into-training-and-testing-sets"></a>將分割區為定型集和測試集  
  
1.  在 **資料採礦**功能區中，按一下**範例資料**。  
  
2.  在 **選取來源資料**頁面上，指定是否**資料**您想要的磁碟分割是在 Excel 範圍或資料表，還是在外部資料來源。  
  
3.  在 **選取取樣類型**頁面上，指定是否要建立定型和測試資料集隨機取樣，或透過超取樣建立新的資料集。  
  
    > [!NOTE]  
    >  如果您使用的是外部資料來源，則僅能使用隨機取樣選項。 如果想到搭配外部資料使用超取樣，您可以使用 Excel 資料連接，將資料匯入到 Excel 活頁簿，然後再使用 [取樣資料精靈]。  
  
4.  設定所選取樣方法的特定選項。  
  
    -   若是隨機取樣，指定要用於測試之原始資料的百分比，或是要在測試資料集中使用之資料列的總數。  
  
    -   若是超取樣，則選取您要強調的資料行和值。 然後，在新資料集中指定資料列的總數，以及在新資料集中，應該包含目標值之資料列的百分比。  
  
         超取樣的目標值必須是離散值；您無法超取樣連續數值資料。  
  
5.  在  **完成 頁面**，接受預設名稱，新的資料集，或輸入新名稱。  
  
     此精靈會為每個資料集建立新的工作表。  
  
 適用於 Excel 的資料採礦用戶端中大部分的精靈也提供將資料隨機分割為定型與測試資料集的選項。 但是，如果您使用這些精靈，您的資料會保留在相同的工作表 (或其他資料來源) 中，而關於特定資料列為測試案例或定型案例的相關資訊，則會儲存在內部。 相反地，當您使用**範例資料**精靈時，測試與定型資料會輸出到個別工作表，讓您可以輕鬆參考。  
  
## <a name="related-options"></a>相關的選項  
 當您逐步進行精靈時，會有下列選項：  
  
|選項。|註解|  
|-------------|--------------|  
|選取來源資料對話方塊 (適用於 Excel 的資料採礦用戶端)|選取包含資料的 Excel 範圍或資料表。 如果您要使用外部資料，可以使用關聯式資料，不過資料必須包含在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源中。 T|  
|選取取樣類型頁面 (適用於 Excel 的資料採礦用戶端)|如果您使用外部資料來源，則僅能使用隨機取樣選項。 此外，您必須指定要使用最終資料集，在建立資料列數目**資料列計數**選項。 您無法指定來源資料的百分比。|  
|隨機取樣頁面 (適用於 Excel 的資料採礦用戶端)|您可以從來源複製某個百分比的資料列，或特定資料列數目。|  
|超取樣頁面 (適用於 Excel 的資料採礦用戶端)|**目標狀態**<br /><br /> 從清單選取原始資料集中低於適當比例的值。 超取樣將會增加包含此狀態之資料列的比例。<br /><br /> **取樣大小**<br /><br /> 選取要擷取的資料列總數。 這個值代表最終資料集的大小。|  
  
## <a name="other-sampling-options"></a>其他取樣選項  
 如果此精靈中的取樣選項不符合您的需要，您可以使用 SQL Server Integration Services (SSIS) 中的取樣轉換來取樣多個資料來源的資料列。  
  
 如需詳細資訊，請參閱 < [Row Sampling Transformation](../integration-services/data-flow/transformations/row-sampling-transformation.md)並[Percentage Sampling Transformation](../integration-services/data-flow/transformations/percentage-sampling-transformation.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦準備檢查清單](checklist-of-preparation-for-data-mining.md)  
  
  
