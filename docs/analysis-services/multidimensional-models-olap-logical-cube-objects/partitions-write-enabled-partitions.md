---
title: 寫入的分割區 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5bca17d40456d55eb84c6699011547b7f399c05
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="partitions---write-enabled-partitions"></a>資料分割-寫入的資料分割
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cube 中的資料通常是唯讀的； 但是在某些狀況下，您可能會希望資料分割是可寫入的。 可寫入的資料分割可讓商務使用者藉由變更資料格值及分析變更對 Cube 資料的影響，以瀏覽一些狀況。 當您啟用資料分割的寫入功能時，用戶端應用程式可在資料分割中記錄資料的變更。 這些變更稱為回寫資料，是儲存在個別資料表中，不會覆寫量值群組中任何現有的資料。 不過，它們會併入到查詢結果中，就好像它們是 Cube 資料的一部分。  
  
 您可以啟用整個 Cube 或是只有 Cube 中某些資料分割的寫入功能； 可寫入維度是不同但互補的功能。 可寫入的資料分割讓使用者得以更新資料分割資料格，而可寫入維度則讓使用者得以更新維度成員， 您也可以搭配使用這兩項功能。 例如，可寫入的 Cube 或可寫入的資料分割不需要包含任何可寫入的維度。 **相關的主題：**[Write-Enabled 維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)。  
  
> [!NOTE]  
>  如果您想要啟用 Cube 的寫入功能，而這個 Cube 將 Microsoft Access 資料庫當成資料來源，請勿在 Cube、其資料分割或其維度的資料來源定義中使用 Microsoft OLE DB Provider for ODBC Drivers。 而是使用 Microsoft Jet 4.0 OLE DB Provider，或任何含有 Jet 4.0 OLE 的 Jet Service Pack 版本。 如需詳細資訊，請參閱 Microsoft 知識庫文件[濆爧髍孮 Microsoft Jet 4.0 資料庫引擎的最新 service pack](http://support.microsoft.com/?kbid=239114)。  
  
 Cube 可以啟用寫入所有量值使用時才**總和**彙總函式。 連結量值群組和本機 Cube 不可寫入。  
  
## <a name="writeback-storage"></a>回寫儲存  
 商務使用者所做的所有變更都會儲存在回寫資料表中，與目前顯示的值不同。 例如，如果使用者從 90 變更資料格的值為 100，值 **+ 10**儲存在回寫資料表，以及變更與它進行的商務使用者的相關資訊的時間。 累積變更的淨影響會顯示在用戶端應用程式。 將會保留 Cube 中的原始值，並且在回寫資料表中記錄變更的稽核記錄。  
  
 分葉和非分葉資料格的變更，其處理方式不同。 分葉資料格代表量值群組所參考之每個維度中的量值和分葉成員的交集。 分葉資料格的值直接取自事實資料表，且無法向下鑽研來進一步分割。 如果可寫入 Cube 或任何資料分割，則可以對分葉資料格進行變更。 只有在用戶端應用程式提供方法，在構成非分葉資料格的分葉資料格之間散發變更時，才可以變更非分葉資料格。 此處理序叫作配置，是透過多維度運算式 (MDX) 中的 UPDATE CUBE 陳述式加以管理。 商業智慧開發人員可使用 UPDATE CUBE 陳述式來包含配置功能。 如需詳細資訊，請參閱[UPDATE CUBE 陳述式&#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md)。  
  
> [!IMPORTANT]  
>  當更新的資料格未重疊時， **Update Isolation Level** 連接字串屬性可用來增強 UPDATE CUBE 的效能。 如需詳細資訊，請參閱 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>。  
  
 不論用戶端應用程式是否散發非分葉資料格的變更，每當評估查詢時，回寫資料表中的變更都會同時套用至分葉和非分葉資料格，好讓商務使用者可以檢視這些變更對整個 Cube 的影響。  
  
 商務使用者所做的變更會保留在您可以使用的個別回寫資料表中 (如下所示)：  
  
-   轉換至資料分割，以便將變更永久併入到 Cube 中。 這個動作會讓量值群組變成唯讀。 您可以指定篩選運算式來選取您要轉換的變更。  
  
-   捨棄它，使資料分割回到其原始狀態。 此動作使資料分割成為唯讀的。  
  
## <a name="security"></a>Security  
 只有在商務使用者屬於對 Cube 資料格具有讀取/寫入權限的角色時，才可以在 Cube 的回寫資料表中記錄變更。 對於每一個角色，您可以控制哪些 Cube 資料格可以更新，哪些不可以更新。 如需詳細資訊，請參閱[授與 cube 或模型的權限&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟用寫入的維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [彙總和彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [分割區 & #40;Analysis Services-多維度資料 & #41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [啟用寫入的維度](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
