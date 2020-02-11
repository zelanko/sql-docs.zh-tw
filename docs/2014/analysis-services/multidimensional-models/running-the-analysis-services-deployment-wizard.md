---
title: 執行 Analysis Services 部署嚮導 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d8fd34a7e614c1c1bb247f84846e090d22ea053e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073043"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>執行 Analysis Services 部署精靈
  當[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]您使用部署嚮導來[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署專案時，您可以透過下列方式執行嚮導：  
  
-   **以互動方式**以互動方式執行時[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，部署嚮導會根據輸入檔產生 XML 部署腳本，而這些檔案是由使用者輸入以互動方式修改。 精靈只會將使用者修改套用至部署指令碼。 精靈不會修改輸入檔。 如需關於輸入檔的詳細資訊，請參閱 [了解用來建立部署指令碼的輸入檔](deployment-script-files-input-used-to-create-deployment-script.md)。  
  
-   **從命令提示**字元當在命令提示字元下執行時[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，部署嚮導會根據您用來執行嚮導的參數，產生 XML FOR ANALYSIS （XMLA）部署腳本。 此精靈可以是下列其中之一：提示使用者輸入並依據該輸入來修改輸入檔；依現狀使用輸入檔來執行無訊息自動部署；或建立可稍後使用的部署指令碼。  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>以互動方式執行 Analysis Services 部署精靈  
 當您以互動方式執行時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈會從輸入檔讀取值，並呈現此資訊。 您可以修改這些輸入值，例如部署目的地、設定、部署選項和連接字串密碼，或保持原狀。 如果您變更輸入值，在產生 XMLA 部署指令碼時，精靈會使用這些變更。 不過，精靈不會對輸入檔中的值做任何變更。  
  
> [!NOTE]  
>  如果您想要讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈修改輸入值，請在命令提示字元下執行精靈，並設定精靈在回應檔案模式中執行。  
  
 在檢閱輸入值和進行任何變更之前，精靈會產生 XMLA 部署指令碼。 您可以在目的地伺服器上立即執行此部署指令碼，或儲存指令碼供稍後使用。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>以互動方式執行 Analysis Services 部署精靈  
  
-   按一下 **[開始]** 功能表，依序指向 **[所有程式]**、 **[Microsoft SQL Server]** 和 **[Analysis Services]**，然後按一下 **[部署精靈]**。  
  
     -或-  
  
-   在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案的 [**專案**] 資料夾中，按兩下* \<專案名稱>*.asdatabase 檔案。  
  
    > [!NOTE]  
    >  如果您找不到* \<專案名稱>*.asdatabase 檔案，請嘗試使用 [搜尋] 並指定 *. .asdatabase。  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示字元下執行 Analysis Services 部署精靈  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈也可以在命令提示字元下執行。 當您在命令提示字元中執行精靈時，請提供 .asdatabase 檔案的完整路徑，並在下列其中一個模式下執行精靈：  
  
 **回應檔案模式**  
 在回應檔案模式中，精靈可讓您以互動方式修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中建立時原先產生的輸入檔。 在產生 XMLA 部署指令碼之前，精靈會儲存這些修改的輸入檔。 下次執行精靈時，已修改的輸入檔會變成新的起點。  
  
 若要在回應檔案模式中執行嚮導，請使用 **/a**參數。  
  
 **無訊息模式**  
 在無訊息模式中，精靈會依據輸入檔的資訊來執行無訊息自動部署。  
  
 若要在無訊息模式中執行嚮導，請使用 **/s**參數。 當您在無訊息模式中執行精靈時，訊息會輸出到主控台，或是所提供的記錄檔。  
  
 **輸出模式**  
 在輸出模式中，精靈會依據輸入檔產生 XMLA 部署指令碼供稍後執行。  
  
 若要在輸出模式中執行嚮導，請使用 **/o**參數並提供輸出檔名稱。  
  
 如需關於這些命令列參數的詳細資訊，請參閱 [使用部署公用程式的部署模型方案](deploy-model-solutions-with-the-deployment-utility.md)。  
  
 下列程序描述如何在命令提示字元下執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示字元下執行 Analysis Services 部署精靈  
  
1.  開啟命令提示字元，並導覽到 C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE 資料夾。  
  
2.  輸入 **Microsoft.AnalysisServices.Deployment.exe** ，後面接著您要用於執行精靈之模式的對應參數。  
  
## <a name="see-also"></a>另請參閱  
 [瞭解 Analysis Services 部署腳本](understanding-the-analysis-services-deployment-script.md)   
 [使用部署精靈部署模型解決方案](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
