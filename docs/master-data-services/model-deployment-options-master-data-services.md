---
title: "模型部署選項 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf1b17b4-47d5-4eba-83f9-fb0555806867
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 6e4cdd4041ee2065b6cd2aa898068289eda66d9e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="model-deployment-options-master-data-services"></a>模型部署選項 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，當您要部署模型封裝檔案時，必須決定要部署新的或複製的模型，還是更新之前複製的模型。  
  
## <a name="workflows"></a>工作流程  
 在使用模型封裝時，有兩個主要工作流程。  
  
-   在測試環境中建立模型封裝，並且將模型的複製部署到實際執行環境。 經過一段時間後，從測試環境將更新部署到實際執行環境。  
  
-   建立模型封裝，並將它做為新模型部署到相同的環境。 在此情況下，您必須指定模型的新名稱。  
  
## <a name="options"></a>選項。  
 在 MDS 資料庫中，每個模型物件都有唯一識別碼 (ID)。 這些識別碼包含在模型部署封裝中。 當您部署封裝時，必須選擇如何處理這些識別碼。  
  
 下表有助於您在使用系統管理模型部署精靈或 MDSModelDeploy 工具部署模型時，決定選擇。  
  
|選項|說明|注意|  
|------------|-----------------|-----------|  
|新增|建立具有唯一名稱的新模型。 將會建立所有模型物件的新識別碼。|如果建立具有新識別碼的新模型，稍後您無法使用模型部署工具將更新套用至此模型。 在 Web 應用程式中使用精靈來部署模型封裝時，只在已經有相同名稱或識別碼的模型時，您才可以選擇建立新的模型。|  
|複製|建立新的模型，它是封裝中模型的完整複製。 只在此模型不存在於目標環境中 (依名稱或識別碼) 時才有效。 如果要在多個環境中有相同的模型，而且經過一段時間後要更新複製的模式，請使用 [複製]。|這是在 Web 應用程式中精靈的預設行為。 如果已經有相同名稱或識別碼的模型，系統會提示您改為建立新的模型。|  
|Update|以封裝中的模型來更新現有模型。 這兩個模型中的識別碼必須相同。 這是用來更新之前複製的模型。|您只可以更新之前複製的模型 (名稱和識別碼必須相符)。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 MDSModelDeploy 部署模型部署封裝](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)   
 [使用精靈部署模型部署套件](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)   
 [部署模型 &#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
