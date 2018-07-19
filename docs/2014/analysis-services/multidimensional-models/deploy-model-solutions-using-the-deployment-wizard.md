---
title: 使用 「 部署精靈 」 部署模型方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard
- deploying [Analysis Services], Analysis Services Deployment Wizard
- Analysis Services deployments, Analysis Services Deployment Wizard
- Analysis Services Deployment Wizard, about Analysis Services Deployment Wizard
ms.assetid: ff711e8e-971c-43ba-b479-effc034af4a4
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a4c8544aaa91cb9dcfcd248e70a4debd766eb1f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192458"
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Deploy Model Solutions Using the Deployment Wizard
  「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈」使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案產生的 XML 輸出檔做為輸入檔。 這些輸入檔很容易進行修改，以自訂 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的部署。 產生的部署指令碼可以立即執行，或儲存供稍後進行部署使用。  
  
 您可以使用此處討論的精靈來進行部署， 也可以自動化部署或使用同步處理功能。 如果部署的資料庫很龐大，請考慮在目標系統上使用資料分割。 您也可以使用分析管理物件 (AMO)，自動化資料分割的建立與擴展。  
  
> [!IMPORTANT]  
>  如果您針對資料來源或模擬目的在連接字串中指定使用者識別碼或密碼，則 XML 輸出檔或部署指令碼都不會包含這些資訊。 由於在這種狀況下需要使用這些資訊進行處理，所以您將手動加入這些資訊。 如果部署不包含處理，您就可以在部署之後視需要加入此連接和模擬資訊。 如果部署包含處理，您可以在儲存之後於精靈內部或在部署指令碼中加入這項資訊。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題描述如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈、輸入檔以及部署指令碼：  
  
|主題|描述|  
|-----------|-----------------|  
|[執行 Analysis Services 部署精靈](running-the-analysis-services-deployment-wizard.md)|描述可以在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈中執行的各種方式。|  
|[了解用來建立部署指令碼的輸入檔](deployment-script-files-input-used-to-create-deployment-script.md)|描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈使用哪些檔案做為輸入值、這些檔案中包含的內容，以及提供描述如何在這些輸入檔中修改值之主題的連結。|  
|[了解 Analysis Services 部署指令碼](understanding-the-analysis-services-deployment-script.md)|描述部署指令碼的內容，以及指令碼如何執行。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 XMLA 部署模型方案](deploy-model-solutions-using-xmla.md)   
 [同步處理 Analysis Services 資料庫](synchronize-analysis-services-databases.md)   
 [了解用來建立部署指令碼的輸入的檔](deployment-script-files-input-used-to-create-deployment-script.md)   
 [使用部署公用程式部署模型方案](deploy-model-solutions-with-the-deployment-utility.md)  
  
  
