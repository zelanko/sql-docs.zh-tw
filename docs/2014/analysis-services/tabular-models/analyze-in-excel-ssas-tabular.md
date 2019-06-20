---
title: 在 Excel (SSAS 表格式) 中進行分析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8090c75108f7a384019030082699917fca915b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067692"
---
# <a name="analyze-in-excel-ssas-tabular"></a>在 Excel 中進行分析 (SSAS 表格式)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [在 Excel 中進行分析] 功能，為表格式模型製作者提供了一個在開發期間可快速分析模型專案的方法。 [在 Excel 中進行分析] 功能可開啟 Microsoft Excel、建立模型工作空間資料庫的資料來源連接，以及自動將樞紐分析表加入工作表。 工作空間資料庫物件 (資料表、資料行及量值) 會包含在樞紐分析表欄位清單中做為欄位。 接著，即可在有效使用者或角色及檢視方塊的內容中檢視物件及資料。  
  
 本主題假設您已熟悉 Microsoft Excel、樞紐分析表及樞紐分析圖。 若要了解有關使用 Excel 的詳細資訊，請參閱 Excel 說明。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [相關工作](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> 優點  
 [在 Excel 中進行分析] 功能可讓模型製作者利用 Microsoft Excel 這類常見的資料分析應用程式來測試模型專案的功效。 為了使用 [在 Excel 中進行分析] 功能，您必須在與 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]相同的電腦上安裝 Microsoft Office 2003 或更高版本。  
  
> [!NOTE]  
>  如果未將 Office 安裝在與 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]相同的電腦上，您可以在其他電腦上使用 Excel，以連接至工作空間資料庫做為資料來源。 然後即可手動將樞紐分析表加入工作表。  
  
 [在 Excel 中進行分析] 功能可開啟 Excel，並建立一個新的 Excel 活頁簿 (.xls)。 活頁簿至模型工作空間資料庫的資料連接隨即建立。 空白的樞紐分析表會加入活頁簿，且模型物件中繼資料會填入樞紐分析表欄位清單中。 然後，即可將可檢視的資料及交叉分析篩選器加入樞紐分析表。  
  
 依預設，使用 [在 Excel 中進行分析] 功能時，目前登入的使用者帳戶即為有效使用者。 此帳戶通常是管理員，其不受模型物件或資料的檢視限制。 不過，您可以指定其他有效的使用者名稱或角色。 如此可讓您在特定使用者或角色的內容中瀏覽 Excel 內的模型專案。 指定有效的使用者包括下列選項：  
  
 **目前的 Windows 使用者**  
 使用您目前登入的使用者帳戶。  
  
 **其他 Windows 使用者**  
 使用指定的 Windows 使用者名稱，而不是目前登入的使用者。 使用不同的 Windows 使用者並不需要密碼。 物件和資料只能在有效使用者名稱之環境下的 Excel 中進行檢視。 模型物件或資料都無法在 Excel 中進行變更。  
  
 **角色**  
 角色是用來定義物件中繼資料和資料的使用者權限。 角色通常是定義給特定的 Windows 使用者或 Windows 使用者群組。 某些角色可包括 DAX 公式中定義的其他資料列層級篩選。 使用 [在 Excel 中進行分析] 功能時，您可以選擇性地選取要用的角色。 物件中繼資料與資料檢視會受限於針對角色所定義的權限及篩選。 如需詳細資訊，請參閱[建立及管理角色 &#40;SSAS 表格式&#41;](roles-ssas-tabular.md)。  
  
 除了有效的使用者或角色以外，您還可以指定檢視方塊。 檢視方塊可讓模型製作者定義模型物件及資料的特定商務案例檢視。 依預設，不會使用任何檢視方塊。 若要將檢視方塊與 [在 Excel 中進行分析] 搭配使用，檢視方塊必須已透過 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 [檢視方塊] 對話方塊來定義。 若已指定檢視方塊，[樞紐分析表欄位清單] 中只會包含檢視方塊中選取的物件。 如需詳細資訊，請參閱[建立及管理檢視方塊 &#40;SSAS 表格式&#41;](perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> 相關工作  
  
|**主題**|**說明**|  
|---------------|---------------------|  
|[在 Excel 中分析表格式模型 &#40;SSAS 表格式&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)|此主題描述如何使用模型設計師的 [在 Excel 中進行分析] 功能來開啟 Excel、建立模型工作空間資料庫的資料來源連接，以及將樞紐分析表加入工作表。|  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中分析表格式模型 &#40;SSAS 表格式&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [角色 &#40;SSAS 表格式&#41;](roles-ssas-tabular.md)   
 [檢視方塊 &#40;SSAS 表格式&#41;](perspectives-ssas-tabular.md)  
  
  
