---
title: 在 Excel 中分析 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 66b15951e741546ee6f4800603e901a86ff83bcb
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="analyze-in-excel"></a>在 Excel 中分析
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在 SSDT 中，[Excel] 功能中的進行分析表格式模型製作者提供快速分析模型專案，在開發期間的方式。 [在 Excel 中進行分析] 功能可開啟 Microsoft Excel、建立模型工作空間資料庫的資料來源連接，以及自動將樞紐分析表加入工作表。 工作空間資料庫物件 (資料表、資料行及量值) 會包含在樞紐分析表欄位清單中做為欄位。 接著，即可在有效使用者或角色及檢視方塊的內容中檢視物件及資料。  
  
 本文假設您已熟悉 Microsoft Excel、 樞紐分析表及樞紐分析圖。 若要了解有關使用 Excel 的詳細資訊，請參閱 Excel 說明。  
  
##  <a name="bkmk_benefits"></a> 優點  
 [在 Excel 中進行分析] 功能可讓模型製作者利用 Microsoft Excel 這類常見的資料分析應用程式來測試模型專案的功效。 若要使用 excel 中進行分析，您必須將 Microsoft Office 2003 或更新版本與 SSDT 相同的電腦上。  
  
 [在 Excel 中進行分析] 功能可開啟 Excel，並建立一個新的 Excel 活頁簿 (.xls)。 活頁簿至模型工作空間資料庫的資料連接隨即建立。 空白的樞紐分析表會加入活頁簿，且模型物件中繼資料會填入樞紐分析表欄位清單中。 然後，即可將可檢視的資料及交叉分析篩選器加入樞紐分析表。  
  
 依預設，使用 [在 Excel 中進行分析] 功能時，目前登入的使用者帳戶即為有效使用者。 此帳戶通常是管理員，其不受模型物件或資料的檢視限制。 不過，您可以指定其他有效的使用者名稱或角色。 如此可讓您在特定使用者或角色的內容中瀏覽 Excel 內的模型專案。 指定有效的使用者包括下列選項：  
  
 **目前的 Windows 使用者**  
 使用您目前登入的使用者帳戶。  
  
 **其他 Windows 使用者**  
 使用指定的 Windows 使用者名稱，而不是目前登入的使用者。 使用不同的 Windows 使用者並不需要密碼。 物件和資料只能在有效使用者名稱之環境下的 Excel 中進行檢視。 模型物件或資料都無法在 Excel 中進行變更。  
  
 **角色**  
 角色是用來定義物件中繼資料和資料的使用者權限。 角色通常是定義給特定的 Windows 使用者或 Windows 使用者群組。 某些角色可包括 DAX 公式中定義的其他資料列層級篩選。 使用 [在 Excel 中進行分析] 功能時，您可以選擇性地選取要用的角色。 物件中繼資料與資料檢視會受限於針對角色所定義的權限及篩選。 如需詳細資訊，請參閱[建立及管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)。  
  
 除了有效的使用者或角色以外，您還可以指定檢視方塊。 檢視方塊可讓模型製作者定義模型物件及資料的特定商務案例檢視。 依預設，不會使用任何檢視方塊。 若要使用檢視方塊與 在 Excel 中進行分析，檢視方塊必須已定義使用 SSDT 中的 檢視方塊 對話方塊。 若已指定檢視方塊，[樞紐分析表欄位清單] 中只會包含檢視方塊中選取的物件。 如需詳細資訊，請參閱[建立和管理檢視方塊](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|**主題**|**說明**|  
|---------------|---------------------|  
|[在 Excel 中分析表格式模型](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)|本文說明如何使用 Excel 功能，在模型設計師中的 [分析] 來開啟 Excel、 建立模型工作空間資料庫中，資料來源連接以及將樞紐分析表加入至工作表。|  
  
## <a name="see-also"></a>另請參閱  
 [分析在 Excel 中的表格式模型](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
