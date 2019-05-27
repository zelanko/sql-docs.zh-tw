---
title: 選取建立方法 （維度精靈） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d44afc5bb4c352a2cb5dfd39030a52db990e3a0b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069601"
---
# <a name="select-creation-method-dimension-wizard"></a>選取建立方法 (維度精靈)
  使用 **[選取建立方法]** 頁面，即可選取建立維度的方式。  
  
 **若要開啟 維度精靈**  
  
-   在方案總管的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，以滑鼠右鍵按一下 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案的 [維度] 資料夾，然後按一下 [新增維度]。  
  
## <a name="options"></a>選項  
 **使用現有的資料表**  
 根據資料來源中的一個或多個資料表，建立維度。 適用於維度的屬性將會因資料表中資料的結構而不同。  
  
 如需詳細資訊，請參閱 [使用現有的資料表建立維度](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)。  
  
 **資料來源中產生時間資料表**  
 在基礎資料來源中建立時間資料表，然後使用該資料表來建立時間維度。 沒有這類資料表存在，而且您不想要使用指令碼來建立資料表時，請使用此選項。 新的時間資料表將包含您在精靈中指定之日期範圍、屬性和日曆的資料。  
  
> [!NOTE]  
>  若要使用這個選項，您必須擁有在基礎資料來源中建立物件的權限。 如果您沒有在資料來源上建立物件的權限，請嘗試改用 **[在伺服器上產生時間資料表]** 選項。  
  
 如需詳細資訊，請參閱 [產生時間資料表來建立時間維度](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)。  
  
 **產生時間資料表，在伺服器上**  
 直接在伺服器上建立時間資料表，然後使用該資料表來建立時間維度。 如果您沒有在基礎資料來源中建立物件的權限，請使用這個選項。 新的時間維度將包含您在精靈中指定之日期範圍、屬性和日曆的資料。  
  
 如需詳細資訊，請參閱 [產生時間資料表來建立時間維度](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)。  
  
 **在 資料來源中產生非時間資料表**  
 定義不含基礎關聯式資料來源的維度，然後針對資料來源產生必要的結構描述。 這種方法稱為由上而下的模型。  
  
> [!NOTE]  
>  若要使用這個選項，您必須擁有在基礎資料來源中建立物件的權限。  
  
 您可以使用或不使用範本來建立維度。 若要使用範本來建立維度，請從 **[範本]** 清單中選取範本。  
  
 如需詳細資訊，請參閱 [在資料來源中產生非時間資料表來建立維度](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)。  
  
 **範本**  
 選取您想要用來建立維度的範本。 範本會提供一組以特定商業用途為目標的完整屬性和階層定義。  
  
> [!NOTE]  
>  只有在您已經選取 [在資料來源中產生非時間資料表] 時，才能使用這個選項。  
  
## <a name="see-also"></a>另請參閱  
 [維度精靈 F1 說明](dimension-wizard-f1-help.md)   
 [維度&#40;Analysis Services-多維度資料&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多維度模型中的維度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
