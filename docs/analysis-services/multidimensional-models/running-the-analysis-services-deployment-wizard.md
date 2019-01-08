---
title: 執行 Analysis Services 部署精靈 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d459bafe395a10af75f8c0a721f0a8a08f39b3c6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509678"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>執行 Analysis Services 部署精靈
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]透過下列方式可以執行部署精靈：  
  
-   **以互動方式**執行時，以互動方式[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署精靈會產生輸入檔為基礎的部署指令碼，因為由使用者輸入以互動方式修改。 精靈只會將使用者修改套用至部署指令碼。 精靈不會修改輸入檔。 如需關於輸入檔的詳細資訊，請參閱 [了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)。  
  
-   **從命令提示字元**命令提示字元中，當執行[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署精靈會產生部署指令碼，根據您用來執行精靈的參數。 此精靈可以是下列其中之一：提示使用者輸入並依據該輸入來修改輸入檔；依現狀使用輸入檔來執行無訊息自動部署；或建立可稍後使用的部署指令碼。  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>以互動方式執行 Analysis Services 部署精靈  
 當您以互動方式執行時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈會從輸入檔讀取值，並呈現此資訊。 您可以修改這些值這類的輸入作為部署目的地、 組態設定、 部署選項和連接字串密碼-或保留現狀。 如果您變更任何輸入的值時，精靈產生部署指令碼時，就會使用這些變更。 不過，精靈不會對輸入檔中的值做任何變更。  
  
> [!NOTE]  
>  如果您想要讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈修改輸入值，請在命令提示字元下執行精靈，並設定精靈在回應檔案模式中執行。  
  
 在檢閱輸入的值，並進行任何變更之後，精靈就會產生部署指令碼。 您可以在目的地伺服器上立即執行此部署指令碼，或儲存指令碼供稍後使用。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>以互動方式執行 Analysis Services 部署精靈  
  
-   按一下 **開始** > **Microsoft SQL Server** > **部署精靈**。  
  
     -或-  
  
-   在 **專案**的資料夾[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案中，按兩下\<專案名稱 >.asdatabase 檔案。
    > [!NOTE]  
    >  如果您找不到 .asdatabase 檔案，請試著使用 [搜尋] 功能並指定 *.asdatabase。 或者，您可能需要建置在 SSDT 中的專案。  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示字元下執行 Analysis Services 部署精靈  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈也可以在命令提示字元下執行。 當您在命令提示字元中執行精靈時，請提供 .asdatabase 檔案的完整路徑，並在下列其中一個模式下執行精靈：  
  
 **回應檔案模式**  
 在回應檔案模式中，精靈可讓您以互動方式修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立時原先產生的輸入檔。 精靈會儲存這些修改的輸入的檔產生部署指令碼之前。 下次執行精靈時，已修改的輸入檔會變成新的起點。  
  
 若要在回應檔案模式中執行精靈時，使用 **/a**切換。  
  
 **無訊息模式**  
 在無訊息模式中，精靈會依據輸入檔的資訊來執行無訊息自動部署。  
  
 若要執行精靈時以無訊息模式，使用 **/s**切換。 當您在無訊息模式中執行精靈時，訊息會輸出到主控台，或是所提供的記錄檔。  
  
 **輸出模式**  
 在輸出模式中，精靈會產生部署指令碼供稍後執行，依據輸入檔。  
  
 若要在輸出模式下執行精靈時，使用 **/o**切換，並提供輸出檔名稱。  
  
 如需關於這些命令列參數的詳細資訊，請參閱 [使用部署公用程式的部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)。  
  
 下列程序描述如何在命令提示字元下執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示字元下執行 Analysis Services 部署精靈  
  
1.  開啟命令提示字元並瀏覽至 C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio  
  
2.  輸入 **Microsoft.AnalysisServices.Deployment.exe** ，後面接著您要用於執行精靈之模式的對應參數。  
  
## <a name="see-also"></a>另請參閱  
 [了解 Analysis Services 部署指令碼](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
