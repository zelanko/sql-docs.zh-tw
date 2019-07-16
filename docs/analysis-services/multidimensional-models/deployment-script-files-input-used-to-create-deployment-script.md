---
title: 了解用來建立部署指令碼的輸入的檔 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b75ec5d7433931a81a0fa6e2c648f85335fbedc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208970"
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>部署指令碼檔-輸入用來建立部署指令碼
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  當您建置[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]會產生專案檔。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 將這些檔案放入輸出資料夾[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]專案。 依預設，輸出是放在 \Bin 資料夾中。 下表列出 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 建立的 XML 檔案。  
  
|檔案|描述|  
|---------------|-----------------|  
|\<*專案名稱*>.asdatabase|XMLA 檔案的多維度或 1100年/1103年的表格式模型專案或針對表格式 1200年和更高版本的模型專案的 JSON 檔案。 包含專案中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的宣告式定義。|  
|\<*專案名稱*>.deploymenttargets|包含將建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體和資料庫的名稱。|  
|\<*專案名稱*>.configsettings|包含環境特定設定，例如資料來源連接資訊和物件儲存位置。 此檔案中的設定會覆寫中的設定\<*專案名稱*>.asdatabase 檔案。|  
|\<*專案名稱*>.deploymentoptions|包含部署選項，例如部署是否為交易式，以及部署之後是否應處理部署的物件。|  
  
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
  
  
