---
title: "了解用來建立部署指令碼的輸入的檔案 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6dcf9b0c4869542727ed8e29699cddaada4c60e8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>部署指令碼檔案-輸入用來建立部署指令碼
  當您建置[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]產生之專案檔案。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]將這些檔案放入輸出資料夾的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案。 依預設，輸出是放在 \Bin 資料夾中。 下表列出 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 建立的 XML 檔案。  
  
|檔案|Description|  
|---------------|-----------------|  
|\<*專案名稱*>.asdatabase|多維度或 1100年/1103年表格式模型專案、 XMLA 檔案或 JSON 檔案以供表格式 1200年以及更高版本的模型專案。 包含專案中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的宣告式定義。|  
|\<*專案名稱*> placeholder>>.deploymenttargets|包含將建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫的名稱。|  
|\<*專案名稱*> placeholder>>.configsettings|包含環境特定設定，例如資料來源連接資訊和物件儲存位置。 此檔案中的設定會覆寫設定\<*專案名稱*>.asdatabase 檔案。|  
|\<*專案名稱*> 部署|包含部署選項，例如部署是否為交易式，以及部署之後是否應處理部署的物件。|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 絕不會將密碼儲存在專案檔中。  
  
## <a name="modifying-the-input-files"></a>修改輸入檔  
 修改輸入檔中的值或從輸入檔擷取的值會讓您能夠變更部署目的地、 組態設定和部署選項，而不用編輯整個\<*專案名稱*>.asdatabase 檔案 (或整個指令碼檔案，如果您從現有產生的指令碼[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫)。 您可以修改個別的檔案，以輕鬆地針對各種用途建立不同的部署指令碼。  
  
 下列主題說明如何修改各種輸入檔中的值：  
  
-   [指定安裝目標](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [指定資料分割和角色部署選項](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [指定方案部署的組態設定](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [指定處理選項](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行 Analysis Services 部署精靈](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [了解 Analysis Services 部署指令碼](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
